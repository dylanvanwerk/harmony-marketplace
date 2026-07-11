# Design Review

Een zelfstandige Harmony-marketplace-plugin die een **gebouwde** PR/staging-omgeving (of een
**Claude Design prototype**) vergelijkt met het bijbehorende **design**, en een Nederlandstalig
**designer-rapport** met **JIRA-klare tickets** oplevert.

## Waarom

Developers krijgen scherpe, eerlijke feedback of een scherm/feature correct is gebouwd, of dat er
aanpassingen nodig zijn. Design Review meet wat betrouwbaar te meten is, beoordeelt de rest expliciet,
en liegt nooit over de dekking.

## Hoe het werkt

Hybride engine met een **harde scheiding**:

- **`gemeten`** — kleur-ΔE2000, WCAG-contrast, typografie/spacing via `getComputedStyle`, kleur vs.
  Harmony-tokens. Meting draait pas na een geslaagde **ijk-zelftest**; anders geen getal.
- **`beoordeeld/handmatig`** — visuele compositie en interactiegedrag (hover, animatie, toetsenbord,
  responsief). Waar automatiseerbaar wordt interactie tóch gemeten via de Chrome-MCP.

Bevindingen krijgen een 4-traps ernst (🔴/🟠/🟡/⚪), een regelgebaseerd eindoordeel, en gaan door een
**zelfcontrole-loop** die elke 🔴/🟠 probeert te weerleggen vóór het rapport.

## Gebruik

Start met de slash-command:

```
/design-review <optioneel: design-URL en/of PR-URL>
```

…of vraag simpelweg om een review ("review deze PR tegen dit Figma-design"). De skill begeleidt je
door de fasen: intake → Chrome verbinden → koppelen → meten+ijk → beoordelen → zelfcontrole → rapport+tickets.

### Randvoorwaarden

- **Figma-bron:** de Figma MCP moet geautoriseerd zijn (via `/mcp` of je claude.ai-connectorinstellingen).
  Zonder autorisatie werkt in v1 alleen de Claude-Design-prototype-bron end-to-end.
- **Gecodeerde kant:** een verbonden, ingelogde Chrome (Chrome-MCP) met het te reviewen scherm klaargezet.
- **Tokens:** `skills/design-review/references/harmony-foundations.md` is gevuld met de echte
  Harmony-tokens (bron: `harmony-foundations.ai`). Alleen de niet-grijze palet-hexwaarden (blue/yellow/
  green/red/orange/purple) komen nog via de Figma-bron of een latere aanvulling.

## Structuur

```
design-review/
├─ .claude-plugin/plugin.json
├─ SPEC.md                      # de vastgelegde blauwdruk (19 kernbeslissingen + v1-grens)
├─ commands/design-review.md    # /design-review slash-command
└─ skills/design-review/
   ├─ SKILL.md                  # begeleide review-skill (fasen + principes)
   └─ references/
      ├─ meetscripts.md         # vaste, geverifieerde meetscripts + ijk (versiebeheerd)
      ├─ brontypes-en-dekking.md
      ├─ ernst-en-oordeel.md
      ├─ interactie-checklist.md
      ├─ ticket-stijl.md
      ├─ rapport-template.md
      ├─ harmony-foundations.md   # gebundelde kopie (zie kop voor herkomst/versie)
      ├─ harmony-componenten.md   # gebundelde kopie
      ├─ b1-schrijfstijl.md       # gebundelde kopie
      └─ somtoday-terminologie.md # gebundelde kopie
```

## Buiten v1

JIRA-push, pixel-diff, volautomatische matching, Figma Code Connect, zelf inloggen op staging,
beoordeling van subjectieve animatiekwaliteit, en auto-sync van de gebundelde referenties.
Zie `SPEC.md` voor de volledige lijst.

## Onderhoud van de gebundelde referenties

De referenties in `skills/design-review/references/` zijn **kopieën** uit `harmony-os`. Elke kopie
heeft een herkomst/versie-kop. Sync is handmatig (bewuste keuze in v1): werk je de bron bij, kopieer
dan opnieuw en verhoog de `gesynct`-datum in de kop.
