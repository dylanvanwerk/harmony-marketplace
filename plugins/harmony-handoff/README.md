# Harmony-Handoff Plugin

Een bundel skills die de handoff van design naar development bij Topicus Education versnelt en verbetert.

## Skills

### acceptatie-criteria
Schrijft, herschrijft en verscherpt functionele acceptatiecriteria (AC) voor Jira-stories op basis van Figma-designs, screenshots, feature-beschrijvingen of ruwe notities.

**Gebruik:**
- Geef als input: een Figma-link, screenshot, feature-beschrijving, of ruwe bullets.
- De skill vraagt bij korte/ambigue input of je een complete story wilt uitwerken of alleen de tekst wilt verscherpen.

**Triggers (automatisch):**
- "schrijf de AC voor..."
- "verscherp deze criteria"
- "herschrijf de AC"
- "maak een Jira-story"
- "werk deze user story uit"

### design-review
Vergelijkt een gebouwde PR/staging-omgeving (of Claude Design prototype) met het bijbehorende design en levert een Nederlandstalig designer-rapport met JIRA-klare tickets. Hybride engine met een harde scheiding tussen **gemeten** (ΔE2000, WCAG-contrast, `getComputedStyle`, tokens) en **beoordeeld/handmatig** (visuele compositie, interactiegedrag). Bevindingen krijgen een 4-traps ernst (🔴/🟠/🟡/⚪) en gaan door een zelfcontrole-loop die elke 🔴/🟠 probeert te weerleggen vóór het rapport.

**Gebruik:**
```
/harmony-handoff:design-review <optioneel: design-URL en/of PR-URL>
```
…of vraag simpelweg om een review ("review deze PR tegen dit Figma-design"). De skill begeleidt je door de fasen: intake → Chrome verbinden → koppelen → meten+ijk → beoordelen → zelfcontrole → rapport+tickets. Zie `skills/design-review/SPEC.md` voor de volledige blauwdruk en de v1-grenzen.

**Randvoorwaarden:**
- **Figma-bron:** de Figma MCP moet geautoriseerd zijn. Zonder autorisatie werkt in v1 alleen de Claude-Design-prototype-bron end-to-end.
- **Gecodeerde kant:** een verbonden, ingelogde Chrome (Chrome-MCP) met het te reviewen scherm klaargezet.
- **Tokens:** `skills/design-review/references/harmony-foundations.md` moet gevuld zijn met de echte Harmony-tokens.

**Onderhoud van de gebundelde referenties:** de referenties in `skills/design-review/references/` zijn **kopieën** uit `harmony-os`. Sync is handmatig — werk je de bron bij, kopieer dan opnieuw en verhoog de `gesynct`-datum in de kop van elk bestand.

## Installatie via GitHub marketplace

Zie de organisatie-admin voor toegang via de Topicus Education plugin marketplace.
