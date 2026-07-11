# Ernst-classificatie & eindoordeel

## Ernstschaal (4-traps)

| Ernst | Wanneer | Voorbeelden |
|---|---|---|
| 🔴 **Kritiek** | Functioneel of toegankelijkheid gebroken | Ontbrekende/verkeerde functionaliteit of component uit het design; contrast **onder** WCAG-minimum (< 4,5:1 normaal, < 3:1 groot); verkeerde Harmony-component |
| 🟠 **Belangrijk** | Duidelijk zichtbare afwijking | ΔE2000 **> 3**; hardcoded hex zonder token; fout token; verkeerde variant/state; fors afwijkende spacing/typografie |
| 🟡 **Klein** | Subtiele afwijking net boven meetruis | ΔE2000 **1–3**; 1–2px spacing-verschil; cosmetisch |
| ⚪ **Observatie / handmatig** | Niet gemeten, vraagt menselijke check | Animatie-kwaliteit, hover-microinteractie, screenreader-gedrag, of elke bevinding waarvan het bewijs/koppeling **onzeker** is |

### Drempels (hard)
- **ΔE2000:** > 3 → 🟠 · 1–3 → 🟡 · < 1 → geen bevinding (binnen meetruis).
- **Contrast:** < drempel (4,5:1 / 3:1) → 🔴. Meet met Script 3.
- **Spacing/typografie:** benoem het verschil in px/waarde; ernst volgt uit de grootte en zichtbaarheid.

### Verplichte velden per bevinding
Elke bevinding bevat:
1. **Ernst** (🔴/🟠/🟡/⚪)
2. **Label** — `gemeten` of `beoordeeld/handmatig`
3. **Categorie** — Visuele gelijkenis · Typografie & spacing · Kleur & tokens · Contrast · Componentgebruik · Interactie
4. **Bewijs** — waarde in design vs. waarde in code + **bron** (bijv. "getComputedStyle op `.card__title`", "get_variable_defs", "screenshot"). Bij `gemeten`: het exacte getal én de bevestigde selector.
5. **Aanbeveling** — wat moet er gebeuren (welk token/component/waarde).

## Regelgebaseerd eindoordeel

Bepaal per **review-eenheid** én **overall** (overall = strengste eenheid):

| Aanwezige ernst | Eindoordeel |
|---|---|
| 1 of meer 🔴 | **Afgekeurd — aanpassingen nodig** |
| Geen 🔴, wel 1+ 🟠 | **Aanpassingen nodig** |
| Alleen 🟡 en/of ⚪ | **Akkoord met kanttekeningen** |
| Geen bevindingen | **Akkoord** |

Open ⚪ handmatige checks worden **altijd apart** benoemd als *"nog te verifiëren door mens"* —
zodat een "Akkoord" nooit onterecht overkomt terwijl er nog handmatige checks openstaan.

## Zelfcontrole-loop (verplicht vóór het rapport)

Na de eerste bevindingenronde draait een **tweede, kritische verificatiepas** over **elke 🔴 en 🟠**:

1. **Probeer de bevinding te weerleggen.** Vraag actief: klopt de koppeling? Is dit een render-verschil
   i.p.v. een echte afwijking? Meet ik tegen het juiste element/token? Is de ijk geslaagd?
2. **Her-meet / her-inspecteer** het bewijs waar mogelijk (draai het meetscript opnieuw, herbekijk de screenshot).
3. **Uitkomst:**
   - Bevinding **bevestigd** → blijft op zijn ernst.
   - Bevinding **onzeker geworden** → downgrade naar ⚪ met notitie *"na verificatie onzeker"*.
   - Bevinding **weerlegd** → verwijderen, met een korte regel in Dekking & beperkingen waarom.
4. Alleen bevindingen die de tweede pas overleven komen in het definitieve rapport op hun ernst.

**Grondregel:** *geen bewijs, geen bevinding.* Liever een gemiste kleine afwijking dan een valse kritieke.
