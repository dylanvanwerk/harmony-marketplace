# Meetscripts — geverifieerde meting (versiebeheerd)

> **Status: vast asset. Wijzig alleen bewust en verhoog dan de versie hieronder.**
> Claude schrijft deze scripts NIET per run opnieuw. Injecteer ze letterlijk in de pagina
> via de Chrome-MCP (`javascript_tool`) en gebruik de resultaten.
>
> **versie:** 1.0.0 · **laatst geverifieerd:** 2026-07-10

Deze scripts leveren de `gemeten`-helft van de review. Alles wat hiermee gemeten wordt,
krijgt in het rapport het label **`gemeten`** met de exacte waarde en bron. Alles daarbuiten
is **`beoordeeld/handmatig`**.

## Harde regel: ijk vóór meting

**Vóór élke review draait `DR_selftest()`.** Slaagt de zelftest niet volledig, dan levert de
plugin GEEN meetgetallen op — elke betrokken bevinding wordt gedowngraded naar ⚪ met de
melding *"meting niet betrouwbaar — ijk gefaald"*. Nooit een getal verzinnen.

De zelftest ijkt drie pijlers met bekende referentiewaarden:
1. **Kleurconversie** sRGB → CIELAB (D65): `#ffffff → L≈100, a≈0, b≈0`; `#000000 → L≈0`.
2. **ΔE2000** (CIEDE2000): identieke kleur → `0`; Sharma-referentiepaar #1 → `2.0425`.
3. **WCAG-contrast**: `#000/#fff → 21.00`; `#fff/#fff → 1.00`; `#767676/#fff → 4.54`; `#777777/#fff → 4.48`.

Referentiebron ΔE2000: Sharma, Wu & Dalal (2005), *The CIEDE2000 color-difference formula*,
supplementaire testdata. Verifieer de referentiewaarde bij twijfel tegen die bron.

---

## Script 1 — Kernbibliotheek (kleur, ΔE2000, contrast, ijk)

Injecteer dit als eerste. Het definieert `window.DR` en draait niets uit zichzelf.

```js
(() => {
  const DR = {};

  // ---- Kleur parsen: elke CSS-kleur → {r,g,b,a} in 0..255 / 0..1 ----
  // Gebruik de browser zelf als parser (dekt hex, rgb(), hsl(), named, etc.)
  DR.parseColor = (css) => {
    if (!css) return null;
    const el = document.createElement('span');
    el.style.color = '';
    el.style.color = css;
    if (el.style.color === '') return null;       // ongeldige kleur
    el.style.display = 'none';
    document.body.appendChild(el);
    const cs = getComputedStyle(el).color;         // altijd "rgb(a)(...)"
    document.body.removeChild(el);
    const m = cs.match(/rgba?\(([^)]+)\)/);
    if (!m) return null;
    const p = m[1].split(',').map(s => parseFloat(s.trim()));
    return { r: p[0], g: p[1], b: p[2], a: p[3] === undefined ? 1 : p[3] };
  };

  // ---- sRGB kanaal → lineair ----
  const lin = (c) => { c /= 255; return c <= 0.04045 ? c / 12.92 : Math.pow((c + 0.055) / 1.055, 2.4); };

  // ---- Relatieve luminantie (WCAG) ----
  DR.luminance = ({ r, g, b }) => 0.2126 * lin(r) + 0.7152 * lin(g) + 0.0722 * lin(b);

  // ---- WCAG-contrastratio tussen twee kleuren ----
  DR.contrast = (c1, c2) => {
    const L1 = DR.luminance(c1), L2 = DR.luminance(c2);
    const hi = Math.max(L1, L2), lo = Math.min(L1, L2);
    return (hi + 0.05) / (lo + 0.05);
  };

  // ---- sRGB → XYZ → CIELAB (D65) ----
  DR.rgbToLab = ({ r, g, b }) => {
    const R = lin(r), G = lin(g), B = lin(b);
    // sRGB → XYZ (D65)
    let X = R * 0.4124564 + G * 0.3575761 + B * 0.1804375;
    let Y = R * 0.2126729 + G * 0.7151522 + B * 0.0721750;
    let Z = R * 0.0193339 + G * 0.1191920 + B * 0.9503041;
    // normaliseren op D65 witpunt
    X /= 0.95047; Y /= 1.00000; Z /= 1.08883;
    const f = (t) => t > 0.008856 ? Math.cbrt(t) : (7.787 * t) + (16 / 116);
    const fx = f(X), fy = f(Y), fz = f(Z);
    return { L: (116 * fy) - 16, a: 500 * (fx - fy), b: 200 * (fy - fz) };
  };

  // ---- CIEDE2000 (ΔE2000) tussen twee Lab-kleuren ----
  DR.deltaE2000 = (lab1, lab2) => {
    const { L: L1, a: a1, b: b1 } = lab1;
    const { L: L2, a: a2, b: b2 } = lab2;
    const rad = Math.PI / 180, deg = 180 / Math.PI;
    const C1 = Math.hypot(a1, b1), C2 = Math.hypot(a2, b2);
    const Cbar = (C1 + C2) / 2;
    const G = 0.5 * (1 - Math.sqrt(Math.pow(Cbar, 7) / (Math.pow(Cbar, 7) + Math.pow(25, 7))));
    const a1p = (1 + G) * a1, a2p = (1 + G) * a2;
    const C1p = Math.hypot(a1p, b1), C2p = Math.hypot(a2p, b2);
    const h = (x, y) => { let hp = Math.atan2(y, x) * deg; return hp < 0 ? hp + 360 : hp; };
    const h1p = (C1p === 0) ? 0 : h(a1p, b1);
    const h2p = (C2p === 0) ? 0 : h(a2p, b2);

    const dLp = L2 - L1;
    const dCp = C2p - C1p;
    let dhp;
    if (C1p * C2p === 0) dhp = 0;
    else {
      dhp = h2p - h1p;
      if (dhp > 180) dhp -= 360;
      else if (dhp < -180) dhp += 360;
    }
    const dHp = 2 * Math.sqrt(C1p * C2p) * Math.sin((dhp * rad) / 2);

    const Lbarp = (L1 + L2) / 2;
    const Cbarp = (C1p + C2p) / 2;
    let hbarp;
    if (C1p * C2p === 0) hbarp = h1p + h2p;
    else {
      hbarp = h1p + h2p;
      if (Math.abs(h1p - h2p) > 180) hbarp += (hbarp < 360 ? 360 : -360);
      hbarp /= 2;
    }
    const T = 1 - 0.17 * Math.cos((hbarp - 30) * rad) + 0.24 * Math.cos((2 * hbarp) * rad)
              + 0.32 * Math.cos((3 * hbarp + 6) * rad) - 0.20 * Math.cos((4 * hbarp - 63) * rad);
    const dtheta = 30 * Math.exp(-Math.pow((hbarp - 275) / 25, 2));
    const Rc = 2 * Math.sqrt(Math.pow(Cbarp, 7) / (Math.pow(Cbarp, 7) + Math.pow(25, 7)));
    const Sl = 1 + (0.015 * Math.pow(Lbarp - 50, 2)) / Math.sqrt(20 + Math.pow(Lbarp - 50, 2));
    const Sc = 1 + 0.045 * Cbarp;
    const Sh = 1 + 0.015 * Cbarp * T;
    const Rt = -Math.sin((2 * dtheta) * rad) * Rc;

    return Math.sqrt(
      Math.pow(dLp / Sl, 2) +
      Math.pow(dCp / Sc, 2) +
      Math.pow(dHp / Sh, 2) +
      Rt * (dCp / Sc) * (dHp / Sh)
    );
  };

  // ---- Gemak: ΔE2000 direct tussen twee CSS-kleuren ----
  DR.deltaEcss = (css1, css2) => {
    const c1 = DR.parseColor(css1), c2 = DR.parseColor(css2);
    if (!c1 || !c2) return null;
    return DR.deltaE2000(DR.rgbToLab(c1), DR.rgbToLab(c2));
  };

  // ---- Zelftest / ijk ----
  DR.selftest = () => {
    const near = (x, y, tol) => Math.abs(x - y) <= tol;
    const checks = [];

    // 1. Kleurconversie
    const white = DR.rgbToLab({ r: 255, g: 255, b: 255, a: 1 });
    const black = DR.rgbToLab({ r: 0, g: 0, b: 0, a: 1 });
    checks.push(['lab-white-L', near(white.L, 100, 0.5), white.L]);
    checks.push(['lab-white-a', near(white.a, 0, 0.5), white.a]);
    checks.push(['lab-white-b', near(white.b, 0, 0.5), white.b]);
    checks.push(['lab-black-L', near(black.L, 0, 0.5), black.L]);

    // 2. ΔE2000
    const dIdent = DR.deltaE2000({ L: 50, a: 2.6772, b: -79.7751 }, { L: 50, a: 2.6772, b: -79.7751 });
    checks.push(['de00-identical', near(dIdent, 0, 1e-6), dIdent]);
    const dSharma1 = DR.deltaE2000({ L: 50, a: 2.6772, b: -79.7751 }, { L: 50, a: 0, b: -82.7485 });
    checks.push(['de00-sharma1', near(dSharma1, 2.0425, 0.001), dSharma1]);

    // 3. WCAG-contrast
    const cBW = DR.contrast({ r: 0, g: 0, b: 0 }, { r: 255, g: 255, b: 255 });
    checks.push(['contrast-black-white', near(cBW, 21, 0.01), cBW]);
    const cWW = DR.contrast({ r: 255, g: 255, b: 255 }, { r: 255, g: 255, b: 255 });
    checks.push(['contrast-white-white', near(cWW, 1, 0.001), cWW]);
    const c76 = DR.contrast(DR.parseColor('#767676'), { r: 255, g: 255, b: 255 });
    checks.push(['contrast-767676-white', near(c76, 4.54, 0.03), c76]);

    const failed = checks.filter(c => !c[1]);
    return { ok: failed.length === 0, checks, failed };
  };

  window.DR = DR;
  return 'DR geladen';
})();
```

**Aanroep ijk:** evalueer `window.DR.selftest()`. Verwacht `{ ok: true, ... }`.
Bij `ok: false` → stop de meting, rapporteer welke checks faalden, downgrade betrokken
bevindingen naar ⚪.

---

## Script 2 — Element-extractie (getComputedStyle per teksttype/element)

Draait ná Script 1, op een reviewer-bevestigde CSS-selector (zie koppeling in de skill).

```js
(sel) => {
  const el = document.querySelector(sel);
  if (!el) return { error: 'selector niet gevonden: ' + sel };
  const cs = getComputedStyle(el);
  const rect = el.getBoundingClientRect();
  const px = (v) => v;                              // waarden komen al in px binnen
  return {
    selector: sel,
    tag: el.tagName.toLowerCase(),
    role: el.getAttribute('role') || null,
    text: (el.textContent || '').trim().slice(0, 120),
    typografie: {
      fontFamily: cs.fontFamily,
      fontSize: cs.fontSize,
      fontWeight: cs.fontWeight,
      lineHeight: cs.lineHeight,
      letterSpacing: cs.letterSpacing,
    },
    spacing: {
      paddingTop: cs.paddingTop, paddingRight: cs.paddingRight,
      paddingBottom: cs.paddingBottom, paddingLeft: cs.paddingLeft,
      marginTop: cs.marginTop, marginRight: cs.marginRight,
      marginBottom: cs.marginBottom, marginLeft: cs.marginLeft,
      gap: cs.gap,
    },
    kleur: {
      color: cs.color,
      backgroundColor: cs.backgroundColor,
      borderColor: cs.borderTopColor,
    },
    vorm: {
      borderRadius: cs.borderTopLeftRadius,
      borderWidth: cs.borderTopWidth,
      boxShadow: cs.boxShadow,
    },
    box: { w: Math.round(rect.width), h: Math.round(rect.height), x: Math.round(rect.x), y: Math.round(rect.y) },
  };
}
```

## Script 3 — Contrast van een tekst-element tegen zijn effectieve achtergrond

Zoekt de eerste voorouder met een niet-transparante achtergrond en meet contrast + WCAG-oordeel.

```js
(sel) => {
  const el = document.querySelector(sel);
  if (!el) return { error: 'selector niet gevonden: ' + sel };
  const cs = getComputedStyle(el);
  const fg = window.DR.parseColor(cs.color);
  // effectieve achtergrond zoeken
  let node = el, bg = null;
  while (node) {
    const b = window.DR.parseColor(getComputedStyle(node).backgroundColor);
    if (b && b.a > 0) { bg = b; break; }
    node = node.parentElement;
  }
  if (!bg) bg = { r: 255, g: 255, b: 255, a: 1 };   // fallback: wit
  const ratio = window.DR.contrast(fg, bg);
  const fontPx = parseFloat(cs.fontSize);
  const bold = parseInt(cs.fontWeight, 10) >= 700;
  const groot = fontPx >= 24 || (fontPx >= 18.66 && bold);   // WCAG "large text"
  const drempel = groot ? 3.0 : 4.5;
  return {
    selector: sel,
    ratio: Math.round(ratio * 100) / 100,
    grootTekst: groot,
    drempel,
    voldoet: ratio >= drempel,
    fgColor: cs.color,
    bgColorGebruikt: node ? getComputedStyle(node).backgroundColor : 'rgb(255,255,255) (fallback)',
  };
}
```

## Script 4 — Alle voorkomende kleuren op de pagina (aggregaat-tokentoets)

Voor de paginaniveau-check: welke kleuren komen voor, zodat je ze tegen de Harmony-tokens houdt.

```js
() => {
  const set = new Map();
  const bump = (c) => { if (!c) return; const p = window.DR.parseColor(c); if (!p || p.a === 0) return;
    const key = `rgb(${Math.round(p.r)}, ${Math.round(p.g)}, ${Math.round(p.b)})`;
    set.set(key, (set.get(key) || 0) + 1); };
  document.querySelectorAll('*').forEach(el => {
    const cs = getComputedStyle(el);
    bump(cs.color); bump(cs.backgroundColor);
    bump(cs.borderTopColor); bump(cs.borderBottomColor);
    bump(cs.borderLeftColor); bump(cs.borderRightColor);
  });
  return [...set.entries()].sort((a, b) => b[1] - a[1]).map(([kleur, aantal]) => ({ kleur, aantal }));
}
```

## Script 5 — Interactie-checks (waar automatiseerbaar)

### 5a. Focus-state zichtbaar?
```js
(sel) => {
  const el = document.querySelector(sel);
  if (!el) return { error: 'niet gevonden: ' + sel };
  const before = getComputedStyle(el);
  const snapshot = (cs) => ({ outline: cs.outlineStyle + ' ' + cs.outlineWidth + ' ' + cs.outlineColor,
    boxShadow: cs.boxShadow, borderColor: cs.borderTopColor, backgroundColor: cs.backgroundColor });
  const b = snapshot(before);
  el.focus();
  const after = getComputedStyle(el);
  const a = snapshot(after);
  const veranderd = JSON.stringify(a) !== JSON.stringify(b);
  return { selector: sel, focusbaar: document.activeElement === el, zichtbareVerandering: veranderd, voor: b, na: a };
}
```

### 5b. Tab-volgorde (focusbare elementen in DOM-volgorde)
```js
() => {
  const sel = 'a[href], button, input, select, textarea, [tabindex]:not([tabindex="-1"])';
  return [...document.querySelectorAll(sel)]
    .filter(el => el.offsetParent !== null && !el.disabled)
    .map((el, i) => ({ i, tag: el.tagName.toLowerCase(), tabindex: el.getAttribute('tabindex'),
      text: (el.textContent || el.getAttribute('aria-label') || '').trim().slice(0, 40) }));
}
```

### 5c. Esc sluit modal / focus-trap
> Dispatch een Escape-keydown en kijk of het modal-element verdwijnt. Selector van de modal
> door de reviewer bevestigd. `hover`-only en animatie-*kwaliteit* zijn NIET automatiseerbaar → ⚪ handmatig.
```js
(modalSel) => {
  const before = !!document.querySelector(modalSel);
  document.dispatchEvent(new KeyboardEvent('keydown', { key: 'Escape', code: 'Escape', bubbles: true }));
  document.activeElement && document.activeElement.dispatchEvent(new KeyboardEvent('keydown', { key: 'Escape', code: 'Escape', bubbles: true }));
  const after = !!document.querySelector(modalSel);
  return { modalSel, aanwezigVoor: before, aanwezigNa: after, escSluit: before && !after };
}
```

### 5d. Responsief gedrag
> Gebruik de Chrome-MCP `resize`-mogelijkheid om de viewport per breekpunt te zetten en dan
> Script 2/3 opnieuw te draaien. Vergelijk de gemeten waarden per viewport.

---

## Wat blijft ⚪ handmatig (niet automatiseerbaar)

- Kwaliteit/timing/easing van animaties en transities.
- Hover-microinteracties die alleen op echte pointer-input betrouwbaar zijn.
- Subjectieve "voelt het goed"-oordelen over beweging en ritme.
- Toegankelijkheid met een echte screenreader (aria-*correctheid* in gebruik).
