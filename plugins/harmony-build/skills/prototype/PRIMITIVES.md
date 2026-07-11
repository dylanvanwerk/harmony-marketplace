# PRIMITIVES — HTML-patronen & interactie-snippets

Bouwblokken voor een `prototype`-artifact. Alle styling komt uit `kit.css` (inline
in `<head>`). Gebruik **echte NL-content** — nooit lorem ipsum, nooit
verzonnen merkstijl. Hou het aantal patronen klein; verzin geen nieuwe.

## Frames

**Desktop** (docent / medewerker):
```html
<div class="wb">
  <div class="topbar"><strong>Somtoday · Cijfers</strong> …</div>
  <!-- inhoud -->
</div>
```

**Mobiel** (leerling / ouder) — altijd in telefoon-frame:
```html
<div class="phone"><div class="phone__screen">
  <div class="phone__notch"></div>
  <div class="phone__body">
    <!-- schermen -->
  </div>
  <nav class="bottomnav">
    <button aria-current="page">Rooster</button>
    <button data-dead>Cijfers</button>
    <button data-dead>Berichten</button>
  </nav>
</div></div>
```

## Componenten (kies uit deze set)

- **Kaart**: `<div class="card stack"> … </div>`
- **Lijst**: `<ul class="list"><li class="row row--between"> … </li></ul>`
- **Tabel**: standaard `<table>` (grijs, dunne lijnen).
- **Form-field**: `<div class="field"><label>…</label><input></div>`
- **Knop**: `.btn` (secundair), `.btn--primary` (dé hoofdactie, max één per scherm), `.btn--ghost`.
- **Badge**: `.badge` / `.badge--accent`.
- **Placeholder-beeld**: `<div class="ph">Foto</div>` (kruis-blok, nooit een echte afbeelding).
- **Tabs**: `.tabbar` met `aria-selected`.

## "Buiten scope" (happy-path regel)

Alles wat niet op het hoofdpad ligt: laat het **zien** maar zet het inactief.
```html
<button class="btn" data-dead title="Buiten scope van deze prototype">Exporteren</button>
```

## Interactie-snippets (vanilla JS, onderaan `<body>`)

**Schermnavigatie** — meerdere schermen in één artifact:
```html
<section class="screen is-active" id="s1"> … <button data-goto="s2">Volgende</button></section>
<section class="screen" id="s2"> … <button data-goto="s1">Terug</button></section>
<script>
  document.addEventListener('click', e => {
    const t = e.target.closest('[data-goto]'); if (!t) return;
    document.querySelectorAll('.screen').forEach(s => s.classList.remove('is-active'));
    document.getElementById(t.dataset.goto).classList.add('is-active');
  });
</script>
```

**Menu / submenu** (disclosure):
```html
<div class="menu">
  <button class="btn" aria-expanded="false" data-menu>Meer ▾</button>
  <div class="menu__panel" hidden>
    <button>Aanpassen</button><button>Delen</button>
  </div>
</div>
<script>
  document.addEventListener('click', e => {
    const b = e.target.closest('[data-menu]');
    document.querySelectorAll('.menu__panel').forEach(p => {
      const own = b && b.parentElement.contains(p);
      p.hidden = own ? !p.hidden : true;
    });
    if (b) b.setAttribute('aria-expanded', String(!b.parentElement.querySelector('.menu__panel').hidden));
  });
</script>
```

**Tooltip**: `<span class="tip" tabindex="0" data-tip="Telt 1× mee">gewicht 1</span>`

**Modal**:
```html
<button class="btn" data-open="m1">Openen</button>
<div class="scrim" id="m1" hidden><div class="modal stack"> … <button data-close>Sluiten</button></div></div>
<script>
  document.addEventListener('click', e => {
    const o = e.target.closest('[data-open]'); if (o) document.getElementById(o.dataset.open).hidden = false;
    if (e.target.matches('[data-close]') || e.target.classList.contains('scrim'))
      e.target.closest('.scrim').hidden = true;
  });
</script>
```

**Notitielaag-toggle** (default UIT — schoon voor doelgroeptest):
```html
<button class="btn notes-toggle" data-notes-toggle>Toon notities</button>
<script>
  document.querySelector('[data-notes-toggle]').addEventListener('click', e => {
    const on = document.body.dataset.notes === 'on';
    document.body.dataset.notes = on ? 'off' : 'on';
    e.target.textContent = on ? 'Toon notities' : 'Verberg notities';
  });
</script>
```
Contextuele callout op-canvas: `<span class="callout tip" tabindex="0" data-tip="Waarom deze plek?">1</span>`
(De **inhoudelijke** open vragen horen NIET hier maar in `open-ontwerpvragen.md`.)
