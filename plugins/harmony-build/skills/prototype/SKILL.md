---
name: prototype
description: Bouwt een snelle, goedkope, niet-Harmony medium-fidelity klikbare wireframe (HTML-artifact) om usability te toetsen bij docenten, medewerkers, leerlingen en ouders. Bewust "niet-af" — grayscale + één blauw accent — zodat feedback over flow en begrijpelijkheid gaat i.p.v. styling. USE WHEN de gebruiker snel toetsbaar beeldmateriaal wil van een scherm, flow of los component zonder in Harmony/productie te bouwen; ook bij "maak een prototype/wireframe van…", "hoe zou scherm X eruit kunnen zien", of het toetsen van een taak bij een doelgroep. NIET voor Harmony-fidelity of productie — dat gaat via de Harmony-route.
disable-model-invocation: false
---

# Prototype — medium-fidelity wireframe om op te schieten

Een `prototype` is **bewust niet-af, klikbaar beeld dat één vraag beantwoordt:
kan deze doelgroep deze taak uitvoeren?** Snel en goedkoop, zodat je erop kunt
schieten en het bij docenten/medewerkers/leerlingen/ouders kunt toetsen.

## Wat je oplevert
Twee bestanden in **`docs/[feature]/prototype/`** (altijd die locatie, ook zonder bouwplan):
- `index.html` — self-contained artifact, `kit.css` inline in `<head>`.
- `open-ontwerpvragen.md` — jouw schiet-agenda (zie sjabloon onderaan).

Publiceer `index.html` via de **Artifact-tool** (zelfde pad → zelfde URL bij
redeploy → goedkoop itereren op dezelfde testlink).

## Stap 0 — Intake met stopregel (anti-slop aan de bron)
Bouw **pas** als deze drie helder zijn. Zo niet: stel max 2–3 gerichte vragen, dan bouwen.
1. **Doelgroep** — docent / medewerker / leerling / ouder.
2. **Kern-taak** — welke concrete taak moet iemand kunnen uitvoeren.
3. **Scope** — los component / één scherm / korte flow.

Optionele input, meenemen als aanwezig:
- **Bouwplan-document** (`docs/[feature]/bouwplan.md` of aangewezen) → **leidend** voor scope/schermen/flow; de stopregel geldt dan alleen voor gaten.
- **Referentiescherm** (screenshot / Figma-link) → startpunt voor herontwerp.

## Stap 1 — Design-slot (zachte compositie)
> Laad, **indien beschikbaar**, de skill `Somtoday-Frontend-Design` en pas die
> principes/UX-laws/heuristieken toe. Is die er (nog) niet, gebruik dan
> [BASELINE.md](BASELINE.md) als minimumlat.

Ditzelfde slot regelt later het opschalen naar Harmony. Nu: alleen de baseline.

## Stap 2 — Bouw het artifact
- **Look ligt vast** — plak `kit.css` volledig inline; verzin geen eigen stijl.
  Grayscale + één blauw accent + **échte NL-content** (geen lorem ipsum).
- **Device volgt doelgroep** (overrulebaar): leerling & ouder → mobiel ±375px in
  **telefoon-frame**; docent & medewerker → desktop ±1280px kaal. Eén viewport per artifact.
- **Interactie = happy-path klikbaar**: het hoofdpad werkt; alles daarbuiten
  zichtbaar-maar-`data-dead`. Meerdere schermen in één artifact mag (simpele nav);
  rijkere patronen (menu/submenu/tooltip/modal) waar de taak erom vraagt.
- **Notitielaag**: toggle-knop, **default UIT** (schoon voor doelgroeptest).
  Op-canvas alleen genummerde contextuele callouts. Inhoudelijke vragen → in de MD.
- Bouwblokken en snippets: [PRIMITIVES.md](PRIMITIVES.md). Gebruik die set; verzin geen nieuwe.

## Stap 3 — Publiceer & schrijf de MD
- Publiceer `index.html` via de Artifact-tool.
- Vul `open-ontwerpvragen.md` (sjabloon onder).
- Meld: de artifact-link, de doelgroep + kern-taak, en waar je feedback op wilt.

## Stap 4 — Itereren
Feedback verwerken = **opnieuw draaien op hetzelfde pad** (`docs/[feature]/prototype/`),
zelfde artifact-URL. Verplaats afgehandelde punten in de MD naar "Besloten".

## Grens richting Harmony (harde stop)
Deze skill stopt bij de **goedgekeurde wireframe**. Bouw zelf **geen** Harmony-fidelity.
Bij goedkeuring lever je schone handoff: link naar approved artifact + doelgroep/scope
+ besloten punten (open vragen dicht). Opschalen gebeurt daarna via het slot / de
bestaande Harmony-route (`harmony-os` bouwen, `acceptatie-criteria`, `design-review`).

---

## Sjabloon `open-ontwerpvragen.md`
```markdown
# Open ontwerpvragen — [feature] ([doelgroep])

**Kern-taak:** [welke taak moet [doelgroep] kunnen uitvoeren]
**Scope:** [component / scherm / flow]  ·  **Device:** [mobiel / desktop]
**Artifact:** [link]

## Waar ik feedback op wil (schiet hierop)
1. …
2. …

## Aannames die ik heb gedaan
- …

## Besloten
- (leeg — vult zich tijdens iteraties)
```
