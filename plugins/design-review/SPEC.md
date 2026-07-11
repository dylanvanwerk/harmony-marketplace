# Design Review — Spec (v1)

> Vastgelegde blauwdruk na een `/grill-me`-sessie. Dit document is de bron van waarheid
> voor wat v1 is en waarom. Elke beslissing hieronder is expliciet gemaakt en bevestigd.
> Datum: 2026-07-10 · Auteur: Dylan Foks

## Wat het is

Een **zelfstandige** Harmony-marketplace-plugin die een gebouwde PR/staging-omgeving
(of een Claude Design prototype) vergelijkt met het bijbehorende design, en een
**Nederlandstalig designer-rapport** met **JIRA-klare tickets** oplevert. Doel: developers
scherpe, eerlijke feedback geven of een scherm/feature correct is gebouwd, of dat er
aanpassingen nodig zijn.

## De 19 kernbeslissingen

### Fundament
1. **Vorm** — Volledig zelfstandige plugin (Optie C). Geen afhankelijkheid van `harmony-os`.
   Eigen **gebundelde kopie** van referenties (zie `references/`), elk met herkomst/versie-kop.
2. **Engine** — Hybride met **harde scheiding**. Elke bevinding is `gemeten` of `beoordeeld/handmatig`.
3. **Meetscripts** — Vaste, versiebeheerde assets (`references/meetscripts.md`): ΔE2000,
   WCAG-contrast, getComputedStyle-extractie. Een **ijk-zelftest draait vóór elke review**.
   Faalt de ijk → geen getal, expliciete melding "meting niet betrouwbaar".

### Bronnen & capture
4. **Designbronnen gelijkwaardig** — Figma-URL én Claude Design prototype, beide volwaardig.
   Plugin **detecteert het brontype** en past de reviewset + rapportdekking automatisch aan.
   Dekking wordt expliciet in het rapport benoemd.
5. **Gecodeerde kant** — Reviewer zet een **ingelogde Chrome** klaar op de juiste route.
   Plugin hecht zich via de Chrome-MCP, maakt screenshots en draait meetscripts.
   Plugin vraagt om de te reviewen **viewport(s)**. (Buiten v1: zelf inloggen/navigeren.)
6. **Koppeling** — Reviewer-bevestigd per sectie/element. Claude stelt DOM-kandidaten voor
   (tekst/rol/positie); reviewer bevestigt. (Buiten v1: volautomatische node↔DOM-matching.)

### Reviewpunten
7. **Kleur & tokens** — ΔE2000 gemeten; hardcoded hex zonder token = bevinding.
8. **Typografie & spacing** — font-size/weight/line-height/padding per teksttype (getComputedStyle).
9. **Contrast** — WCAG 4,5:1 / 3:1 als harde grens.
10. **Componentgebruik** — Component + variant + state semantisch getoetst tegen
    `harmony-componenten.md`, gevoed door design-metadata; terugval op "beoordeeld" waar de
    designbron geen componentnaam prijsgeeft. Code Connect niet vereist (nog niet ingericht).
11. **Visuele gelijkenis** — AI-visueel op screenshots (lay-out, structuur, verhoudingen, compositie).
12. **Interactie** — Vaste Harmony-basislijst + scherm-specifieke aanvulling. **Automatisch gemeten
    waar mogelijk** via Chrome-MCP (focus-state zichtbaar, tab-volgorde, Esc/focus-trap in modal,
    gedrag na viewport-resize). Alleen subjectieve animatiekwaliteit blijft ⚪ handmatig.

### Oordeel, kwaliteit & output
13. **Ernst** — 4-traps: 🔴 Kritiek / 🟠 Belangrijk / 🟡 Klein / ⚪ Observatie-handmatig.
    Drempels: ΔE > 3 = belangrijk, ΔE 1–3 = klein; contrast onder WCAG = kritiek.
    Elke bevinding: ernst + label + bewijs (design vs. code + bron) + categorie.
14. **Eindoordeel** — Regelgebaseerd per eenheid + overall:
    1+ 🔴 → *Afgekeurd* · 🟠 (geen 🔴) → *Aanpassingen nodig* · alleen 🟡/⚪ → *Akkoord met kanttekeningen* ·
    niets → *Akkoord*. Open ⚪ apart als "nog te verifiëren door mens".
15. **Eerlijkheid** — "Geen bewijs, geen bevinding" + verplichte downgrade bij twijfel +
    sectie **Dekking & beperkingen**. Plus een **zelfcontrole-loop**: tweede kritische
    verificatiepas die elke 🔴/🟠 probeert te weerleggen; alleen overlevende bevindingen blijven.
16. **Bewijs** — Design- en code-screenshot naast elkaar + meetwaarden-tabel, in een **aparte werkmap**
    (`design-review/<datum>-<eenheid>/`). Geen pixel-diff in v1.
17. **Rapport** — Markdown, feitelijk professioneel NL, geschreven **vanuit de stem van een Designer**
    die developers constructieve feedback geeft. Apart tickets-blok in de handoff-stijl
    (🔴/🟠 → concept-tickets, 🟡/⚪ → keuzelijst). Geen JIRA-push in v1 (copy-paste).

### Scope per run & entry point
18. **Scope** — Review-eenheid = één frame ↔ één schermstaat; meerdere eenheden per sessie;
    één geaggregeerd rapport met samenvatting bovenaan.
19. **Entry point** — Eén begeleide skill `design-review` + `/design-review` slash-command.
    Vaste fasen met bevestiging per fase.

## Expliciet buiten v1

- Automatisch pushen naar JIRA (blijft copy-paste; er is nu geen JIRA-koppeling).
- Pixel-overlay/diff-beelden.
- Volautomatische node↔DOM- en scherm↔scherm-matching.
- Figma Code Connect-integratie.
- Automatisch inloggen op / navigeren binnen staging.
- Beoordeling van subjectieve animatie-*kwaliteit* (blijft handmatig).
- Auto-sync van de gebundelde Harmony-referenties (handmatige sync met versie-kop).

## Bekende randvoorwaarden

- **Figma MCP moet geautoriseerd zijn** voor de Figma-URL-bron. Zonder autorisatie werkt in v1
  alleen de Claude-Design-prototype-bron end-to-end. Autoriseren via `/mcp` (interactieve sessie)
  of de claude.ai-connectorinstellingen.
- **Chrome-MCP vereist een verbonden, ingelogde Chrome** met het te reviewen scherm klaargezet.
- **`harmony-foundations.md` is gevuld** met de echte Harmony-tokens (bron: `harmony-foundations.ai`,
  key `tzrSfWlGdh1O3KOoxQijWk`). Eén restpunt: alleen de **grijsschaal**-hexwaarden staan expliciet;
  de exacte hex van blue/yellow/green/red/orange/purple-stappen komt via de Figma-bron
  (`get_variable_defs`) of wordt later aangevuld. Zolang die ontbreken → plugin meldt dit i.p.v. te verzinnen.
