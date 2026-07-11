---
name: design-review
description: >
  Vergelijkt een gebouwde PR/staging-omgeving (of Claude Design prototype) met het bijbehorende
  design en levert een Nederlandstalig designer-rapport met JIRA-klare tickets. Gebruik deze skill
  wanneer de gebruiker een gebouwde feature/scherm wil laten reviewen tegen een design — bij
  zinnen als "review deze PR tegen dit design", "design review", "vergelijk staging met Figma",
  "klopt de build met het ontwerp", "toets dit scherm tegen het prototype", of wanneer een
  design-URL (Figma of Claude Design prototype) samen met een staging/PR-URL wordt aangeleverd.
  Triggert ook op de slash-command /design-review.
metadata:
  author: Dylan Foks
  version: "0.1.0"
---

# Design Review

Je begeleidt een designer door een review waarin een **gebouwde** omgeving (PR/staging of Claude
Design prototype) wordt vergeleken met het **design**, en levert een Nederlandstalig rapport met
JIRA-klare tickets. Zie `SPEC.md` (in deze skill-map) voor de volledige blauwdruk en de v1-grenzen.

## Kernprincipes (altijd)

1. **Harde scheiding gemeten vs. beoordeeld.** Elke bevinding krijgt het label `gemeten`
   (met exacte waarde + bron) of `beoordeeld/handmatig`. Nooit een AI-inschatting als meting presenteren.
2. **Geen bewijs, geen bevinding.** Bij twijfel over koppeling of meting → downgrade naar ⚪, niet 🔴/🟠.
3. **IJk vóór meting.** Draai `DR.selftest()` vóór elke meetronde. Faalt de ijk → geen meetgetallen.
4. **Reviewer bevestigt de koppeling.** Jij stelt DOM-kandidaten voor; de mens bevestigt welke
   Figma-node ↔ welk DOM-element hoort. Nooit stilzwijgend automatisch koppelen.
5. **Stem van een Designer.** Feitelijk, professioneel Nederlands, constructief. Engelse
   componentnamen en handoff-opmaak voor de tickets (zie `references/ticket-stijl.md`).
6. **Bevestig per fase.** Loop de fasen hieronder één voor één; sluit elke fase af met een korte
   bevestiging bij de reviewer voordat je doorgaat.

## Referenties (laad wat je nodig hebt)

- `references/meetscripts.md` — vaste meetscripts (ΔE2000, contrast, getComputedStyle, ijk). **Niet herschrijven.**
- `references/brontypes-en-dekking.md` — brontype-detectie en wat per bron toetsbaar is.
- `references/ernst-en-oordeel.md` — ernstschaal, drempels, eindoordeel, zelfcontrole-loop.
- `references/interactie-checklist.md` — vaste basislijst + scherm-specifieke aanvulling.
- `references/ticket-stijl.md` — JIRA-klare tickets in de handoff-stijl.
- `references/rapport-template.md` — de exacte rapportstructuur.
- `references/harmony-foundations.md` — **strikt toegestane tokens** (tokentoets). Als leeg → meld dat.
- `references/harmony-componenten.md` — toegestane componenten (componenttoets).
- `references/somtoday-terminologie.md` — verplichte terminologie in rapport + tickets.
- `references/b1-schrijfstijl.md` — alleen voor geciteerde eindgebruikersteksten.

## Randvoorwaarden (check vroeg)

- **Figma-bron** vereist een geautoriseerde Figma MCP. Niet geautoriseerd → meld het en werk met de
  Claude-Design-prototype-bron, of vraag een screenshot-export.
- **Gecodeerde kant** vereist een verbonden, ingelogde Chrome (Chrome-MCP) met het scherm klaargezet.
- Reviewuitvoer landt in een **aparte werkmap**: `design-review/<datum>-<eenheid>/` met
  `design.png`, `code.png` en `rapport.md`.

---

## Fasen

### Fase 0 — Intake & brontype-detectie
1. Vraag (of herken uit de input): **design-bron-URL** en **PR/staging-URL**.
2. Detecteer het brontype (zie `references/brontypes-en-dekking.md`) en bevestig het bij de reviewer.
3. Bepaal en benoem meteen de **verwachte dekking**: wat wél/niet toetsbaar is bij deze bron
   (bv. "Figma niet geautoriseerd → geen `get_variable_defs`, we toetsen tegen Harmony-foundations").
4. Vraag welke **review-eenheden** (frame ↔ schermstaat) in deze sessie meegaan, en welke **viewport(s)**.
5. Maak de werkmap(pen) aan.

### Fase 1 — Chrome verbinden & scherm klaarzetten
1. Vraag de reviewer de **ingelogde Chrome** op de juiste route/staat te zetten, per viewport.
2. Hecht je via de Chrome-MCP, zet de viewport, maak `code.png` (screenshot) per eenheid.
3. Bij een Claude Design prototype: open ook de **design-DOM** (tweede tab/URL) voor DOM-vs-DOM-meting.
4. Bij een Figma-bron: haal `get_screenshot`, `get_metadata`, en (indien beschikbaar)
   `get_variable_defs` + `get_design_context` op. Sla het design-referentiebeeld op als `design.png`.

### Fase 2 — Koppelen (per eenheid, reviewer bevestigt)
1. Stel per sectie/element DOM-kandidaten voor op basis van tekst/rol/positie.
2. Laat de reviewer de koppeling **bevestigen** (Figma-node/design-element ↔ CSS-selector).
3. Leg de bevestigde koppelingen vast; die vormen de basis voor de metingen.

### Fase 3 — Meten (+ ijk)
1. Injecteer **Script 1** (kernbibliotheek) en draai `DR.selftest()`. **Faalt de ijk → geen meetgetallen**,
   meld welke checks faalden, en downgrade de betrokken bevindingen naar ⚪.
2. Draai per bevestigde koppeling **Script 2** (typografie/spacing/kleur/vorm), **Script 3** (contrast),
   en waar relevant **Script 4** (paginaniveau-kleuren) en **Script 5** (interactie).
3. Vergelijk gemeten code-waarden met de design-waarden en met de tokens:
   - **Kleur:** ΔE2000 (drempels in `ernst-en-oordeel.md`); hardcoded hex zonder token = bevinding.
   - **Typografie & spacing:** verschil per teksttype in px/waarde.
   - **Contrast:** WCAG-oordeel uit Script 3.
   - **Componentgebruik:** component + variant + state tegen `harmony-componenten.md`.
4. Herhaal per viewport waar responsief gedrag een reviewpunt is.

### Fase 4 — Beoordelen (visueel + handmatig)
1. **Visuele gelijkenis:** vergelijk `design.png` ↔ `code.png` (lay-out, structuur, verhoudingen, compositie).
2. **Interactie:** loop de vaste basislijst + scherm-specifieke aanvulling af
   (`references/interactie-checklist.md`); meet met Script 5 waar mogelijk, markeer de rest als ⚪.
3. **Componentgebruik / ontbrekende functionaliteit:** ontbreekt iets dat in het design staat → 🔴.
4. Ken elke bevinding ernst + label + categorie + bewijs + aanbeveling toe (`ernst-en-oordeel.md`).

### Fase 5 — Zelfcontrole-loop
Draai de verplichte tweede verificatiepas over **elke 🔴 en 🟠** (zie `ernst-en-oordeel.md`):
probeer de bevinding te weerleggen, her-meet/her-inspecteer, en downgrade of verwijder wat niet standhoudt.
Log wat je verwijderde in Dekking & beperkingen.

### Fase 6 — Rapport & tickets
1. Bepaal het regelgebaseerde eindoordeel per eenheid + overall (`ernst-en-oordeel.md`).
2. Vul `references/rapport-template.md` volledig in → schrijf `rapport.md` in de werkmap.
3. Zet elke 🔴/🟠 om naar een concept-ticket (`references/ticket-stijl.md`); 🟡/⚪ als keuzelijst.
4. Vul de sectie **Dekking & beperkingen** eerlijk in (brontype, ijk-status, tokenversie, wat niet
   toetsbaar was, open ⚪ checks).
5. Presenteer de kern aan de reviewer en wijs op de werkmap.

## Taal

Nederlands, feitelijk en constructief, vanuit de stem van een Designer. Engelse UI-componentnamen
conform de handoff-conventie. B1-schrijfstijl alleen wanneer het rapport eindgebruikersteksten citeert.
