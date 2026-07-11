# Harmony-Build Plugin

Bouwt snel en goedkoop **medium-fidelity klikbare wireframes** ("prototypes") om usability te toetsen bij doelgroepen (docenten, medewerkers, leerlingen, ouders) — bewust *niet-af* en *niet-Harmony*, zodat feedback over flow en begrijpelijkheid gaat i.p.v. styling.

## Skills

### prototype
Maakt een self-contained, klikbaar HTML-artifact met een **vaste kit** (grayscale + één blauw accent, échte NL-content). Twee granulariteiten: een volledig scherm/flow of een losstaande component. Spaart tijd en tokens door de stijl en interactie-primitives te hergebruiken i.p.v. ze telkens opnieuw te bedenken.

**Gebruik:**
```
/harmony-build:prototype <optioneel: doelgroep, kern-taak, scope>
```
…of vraag simpelweg om een prototype ("maak een prototype van scherm X voor leerlingen"). De skill doorloopt: intake-stopregel → design-slot → bouwen → publiceren → itereren.

**Wat je oplevert** (altijd in `docs/[feature]/prototype/`):
- `index.html` — het artifact, `kit.css` inline. Publiceren via de Artifact-tool (zelfde pad → zelfde URL bij redeploy → goedkoop itereren op dezelfde testlink).
- `open-ontwerpvragen.md` — de schiet-agenda, los van het artifact.

**Triggers (automatisch):**
- "maak een prototype / wireframe van..."
- "hoe zou scherm X eruit kunnen zien"
- "ik wil dit snel toetsen bij [doelgroep]"

**Vaste keuzes:**
- **Look:** medium-fi grayscale + één neutraal blauw accent, échte NL-content, geen merkstijl.
- **Device volgt doelgroep:** leerling & ouder → mobiel in telefoon-frame; docent & medewerker → desktop.
- **Interactie:** happy-path klikbaar; buiten-scope zichtbaar-maar-inactief. Menu/submenu/tooltip/modal waar nodig.
- **Notitielaag:** toggle in het artifact, default uit (schoon voor doelgroeptest).

## Grens richting Harmony

Deze plugin stopt bij de **goedgekeurde wireframe** en levert schone handoff (approved artifact + besluiten + open vragen dicht). Harmony-fidelity en "goed design volgens Somtoday" leven elders:
- **Design-slot:** de skill laadt, indien beschikbaar, `Somtoday-Frontend-Design` (principes, UX-laws, anti-AI-slop); anders geldt de ingebouwde `BASELINE.md`. Ditzelfde slot regelt later het opschalen naar Harmony.
- **Vervolg:** opschalen en QA via de **harmony-handoff**-plugin (`acceptatie-criteria`, `design-review`) en de `harmony-os`-bouw-skills.

## Installatie via GitHub marketplace

Zie de organisatie-admin voor toegang via de Topicus Education plugin marketplace.
