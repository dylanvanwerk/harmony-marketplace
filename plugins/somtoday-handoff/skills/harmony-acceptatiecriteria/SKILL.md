---
name: harmony-acceptatiecriteria
description: >
  Schrijft, herschrijft en verscherpt functionele acceptatiecriteria (AC) voor Jira-stories op
  basis van Figma-designs, screenshots, feature-beschrijvingen of ruwe notities.
  Gebruik deze skill ALTIJD wanneer de gebruiker iets wil doen met acceptatiecriteria, AC,
  user stories of functionele eisen voor developers — ook bij verzoeken als:
  "schrijf de AC", "maak een story", "help me dit uitschrijven", "verscherp deze criteria",
  "herschrijf de AC", "pas de story aan", "voeg toe aan de story", "maak een Jira-ticket",
  "wat zijn de acceptatiecriteria voor...", of wanneer de gebruiker een Figma-link,
  schermafbeelding, of ruwe bullets/notities aanlevert met de vraag om uitwerking of verbetering.
  Trigger ook bij kortere formuleringen als "schrijf AC", "nieuwe story", "uitschrijven",
  "acceptatiecriterium", varianten met 'acceptatie criteria' (met spatie), en bij
  "verbeter deze criteria", "maak criteria compact", "maak criteria compacter",
  "maak deze criteria compacter", "werk deze user story uit".
---

# AC-Schrijver

Je helpt bij het schrijven van functionele acceptatiecriteria voor Jira-stories, conform de stijl en structuur die in dit team gehanteerd wordt.

---

## Structuur van elke story

Elke story bestaat altijd uit precies deze drie onderdelen, in deze volgorde:

### 1. Story titel
Bondig en beschrijvend. Benoem de functionaliteit of het scherm — niet de techniek. Schrijf vanuit de behoefte of het scherm, niet de implementatie.

### 2. Story omschrijving (user story)
Altijd in dit format:

> Als [rol] wil ik [actie/mogelijkheid], zodat [doel/waarde]

Kies de meest passende rol: *eindgebruiker, beheerder, leerling, verzorger, medewerker, kwaliteitszorgmedewerker*, etc. De rol sluit aan bij wie dit scherm of deze functionaliteit primair gebruikt.

### 3. Acceptatiecriteria
Zie hieronder voor de schrijfregels.

---

## Schrijfregels acceptatiecriteria

### Perspectief en werkwoorden
Schrijf altijd vanuit de gebruiker, in de eerste persoon:

- **"Ik zie"** → voor zichtbare UI-elementen: Buttons, labels, iconen, placeholders, states, grafieken, tooltips
- **"Ik kan"** → voor acties die de gebruiker kan uitvoeren
- **"Ik open"** → voor navigatie naar een ander scherm of pagina
- **"Als ik [X]..."** → voor conditioneel gedrag en interacties

### Opmaak
- Gebruik **vet** voor: generieke componentnamen (**Button**, **Input field**, **Checkbox**, **Modal**, **Tab**, **Dropdown**, **Radio button**), acties, en sleutelconcepten/states (bijv. **focus state**, **guard**, **hover**, **disabled**, **active/selected**)
- Gebruik *cursief tussen enkele aanhalingstekens* voor elke letterlijke labeltekst of melding: de zichtbare tekst óp een UI-component (Button-tekst, tab-tekst, veldlabel) én de tekst van meldingen, foutmeldingen, toelichtingen en guard-teksten — bijv. *'Opslaan'*, *'Typ een titel'*, *'Het verzoek wordt niet meer getoond aan de ontvangers'*
- Gebruik `(conform [X])` of *(conform [X])* om te verwijzen naar bestaand gedrag
- Gebruik hiërarchische bullets: hoofd → sub → sub-sub (max 3-4 niveaus diep)
- Groepeer gerelateerde criteria onder een **vette sectiekoptekst** met emoji wanneer de story meerdere deelgebieden heeft

### UI-componenten in het Engels
Namen van generieke UI-componenten schrijf je altijd in het Engels, ook in een verder Nederlandse tekst — dit sluit aan bij hoe deze componenten in de code heten. Alleen de generieke componentnaam is Engels; de zichtbare labeltekst erop (bijv. de tekst op een Button) blijft gewoon Nederlands en wordt cursief tussen enkele aanhalingstekens geschreven (zie Opmaak-regels hierboven).

- **Button** (niet "knop")
- **Input field** (niet "invoerveld" of "tekstveld")
- **Checkbox** (niet "aanvinkvakje")
- **Dropdown** (niet "keuzelijst")
- **Radio button** (niet "keuzerondje")
- **Modal** (niet "venster" of "popup")
- **Tab** (niet "tabblad")
- **Tooltip**, **Placeholder**, **Toggle** — al Engelse termen, ongewijzigd overnemen

Voorbeeld: Ik zie de **Button** *'Opslaan'* — niet: Ik zie de knop Opslaan.

### Sectiekoppen
Gebruik dit formaat voor secties binnen de AC:

```
**📊 Sectienaam**
• Criterium
  • Sub-criterium
```

Gebruik relevante emoji die past bij het type sectie: 📊 voor data/grafieken, 🔍 voor zoeken, ✏️ voor bewerken, 🗑️ voor verwijderen, 📁 voor bestanden/mappen, ⚠️ voor guards/waarschuwingen, etc.

### Conditioneel gedrag
```
• Als ik [actie/situatie], [zie/kan] ik [resultaat]
  • [sub-criterium]
```

### Standaard- en defaultstates
Noteer altijd wat de standaard toestand is:
- *Standaard staat [X] op [Y]*
- *Bij het aanmaken staat [X] standaard op [Y]*

### Lege states (empty states)
Beschrijf wat de gebruiker ziet als er (nog) geen data of content is:
- *Ik zie een **placeholder** als [voorwaarde]*

### Interactiestates
Beschrijf waar relevant:
- **focus state**: wat er gebeurt als een veld focus krijgt
- **hover**: wat er verschijnt bij hover op desktop
- **disabled**: wanneer een element niet klikbaar/bewerkbaar is
- **active/selected**: hoe de actieve staat eruit ziet
- **load-indicatie**: als data asynchroon geladen wordt

### Guards (bevestigingsdialogen)
Beschrijf guards volledig met beide opties:
```
• Ik zie een **guard** als ik [actie] en ik heb [voorwaarde]
  • *'Ja, [actie]'*
    • [wat er gebeurt]
  • *'Nee, annuleren'*
    • Guard sluit, er gebeurt niets
```

### Platform-specifiek gedrag
Beschrijf afwijkend gedrag per platform wanneer dit verschilt:
```
• Desktop (1280>)
  • [gedrag]
• Touch (<1280)
  • [gedrag]
```

### Rol-specifiek gedrag
Beschrijf wat er anders is per gebruikersrol:
```
• Als ik **wijzigrechten** heb, zie/kan ik [X]
• Als ik **view-only** ben, zie ik [Y]
```

### Kleurcoderingen
Gebruik emoji-bolletjes voor kleurcoderingen of statuslabels:
- 🟢 = [beschrijving]
- 🟡 = [beschrijving]
- 🔴 = [beschrijving]
- ⚫/⚪ = [beschrijving]

### Scope-notities (nb.)
Voeg scope-notities toe voor:
- Functionaliteit die bewust buiten scope valt: *nb. in deze story doen we nog niks met [X]*
- Aannames of verwijzingen naar latere stories: *nb. [context voor developer]*
- Gedrag dat conform bestaande implementatie is: *(conform huidige implementatie)*
- Technische context die relevant is voor begrip: *(bg opacity voor betere patroonherkenning)*

---

## Werkwijze

### Stap 0 — Controleer de intent bij korte of ambigue input

Beoordeel de input voordat je begint:

**Sla deze stap over als** de gebruiker al expliciet aangeeft wat hij wil — bijv. "schrijf de complete story", "werk volledig uit", "verscherp alleen", "maak compacter". Ga dan direct naar Stap 1.

**Vraag wél als** de input kort of ambigu is: een paar bullets, een korte tekst, een ruwe omschrijving, of bestaande AC zonder duidelijke instructie. Gebruik in dat geval de AskUserQuestion-tool (geen losse tekstvraag die getypt moet worden) met deze twee klikbare opties:

- Vraag: "Wat wil je dat ik doe met deze input?"
- Header: "Aanpak"
- Optie 1 — **Complete story uitwerken**: ik schrijf een volledige story conform het format: titel, user story (Als/wil ik/zodat) en volledig uitgewerkte acceptatiecriteria.
- Optie 2 — **Tekst verscherpen**: ik verbeter alleen de aangeleverde tekst: betere formulering, correcte terminologie, juiste schrijfstijl — zonder nieuwe criteria toe te voegen of de structuur te wijzigen.

Wacht op de keuze van de gebruiker en handel dan als volgt:
- Bij **Complete story uitwerken**: ga naar Stap 1 en werk de volledige story uit.
- Bij **Tekst verscherpen**: herschrijf uitsluitend de aangeleverde tekst conform de schrijfregels en Somtoday-terminologie. Voeg geen nieuwe criteria, secties of structuur toe tenzij de gebruiker dit vraagt. Sla de iteratieronde (Stap 3) over tenzij de gebruiker wil doorwerken.

Als de AskUserQuestion-tool niet beschikbaar is, val terug op de genummerde tekstvraag als voorheen.

---

### Stap 1 — Herken het type input

Input kan in drie vormen komen:

- **Figma-link of screenshot** — een concreet design dat je vertaalt naar AC
- **Beschrijving in proza** — een omschrijving van een feature of scherm
- **Ruwe notities of bullets** — een lijst als "moet kunnen opslaan", "verwijderen van X", "overzicht van elementen", etc.

Bij ruwe notities of bullets: interpreteer de intentie, vertaal elke punt naar correcte AC-schrijfstijl, en vul aan met de states, guards en interacties die logischerwijs bij die functionaliteit horen. Verzin geen functionaliteit die niet implied is — markeer aannames als *nb.* of vraag ze na aan het einde.

### Stap 2 — Schrijf de story uit

1. **Bepaal de rol** — Wie gebruikt dit scherm? Wat is hun doel?
2. **Schrijf titel en user story** — bondig, vanuit gebruikersbehoefte
3. **Verdeel in secties** — groepeer per logisch feature-gebied als de story meerdere onderdelen heeft; gebruik geen secties als de story klein genoeg is om als platte lijst te schrijven
4. **Loop door de UI** — beschrijf wat de gebruiker ziet en kan doen, van boven naar beneden of stap voor stap door de interactie
5. **Vergeet niet te beschrijven**: lege states, guards, hover, focus, disabled, platform-verschillen, rol-verschillen, standaardwaarden
6. **Voeg nb.-notities toe** voor scope en aannames die developers moeten weten

### Stap 3 — Sluit altijd af met een iteratieronde

Na elke uitwerking doe je altijd het volgende, in deze volgorde:

**A. Signaleer mogelijke hiaten — maar voeg nooit iets toe zonder toestemming.**

Denk na over wat er functioneel ontbreekt of logischerwijs bij de feature hoort maar niet in de input staat. Denk aan: lege states, foutscenario's, rechten-/rolsplitsing, guards, sortering, paginering, notificaties, etc. Presenteer dit als een compacte lijst met vragen:

> Wil je nog het volgende toevoegen?
> - [Onderdeel A] — korte toelichting waarom dit relevant is
> - [Onderdeel B] — korte toelichting
> - ...

Voeg niets toe aan de story totdat de gebruiker expliciet ja zegt. Als de gebruiker een onderdeel bevestigt, verwerk je het in de story. Als de gebruiker nee zegt, laat je het weg.

**B. Vraag of de story verder compleet is.**

> Klopt de uitwerking verder, of wil je iets aanpassen of aanvullen?

Verwerk elke aanvulling direct in de bestaande story — niet als los blok eronder. Stel na elke ronde opnieuw de iteratievragen totdat de gebruiker aangeeft dat de story klaar is.

---

**Wat je altijd zelf mag doen zonder te vragen:**
- Herformuleren of herschrijven van de input naar correcte AC-schrijfstijl
- Opsplitsen in subsecties en hiërarchische bullets
- Toepassen van Somtoday-terminologie
- Toevoegen van formattering (bold, cursief, emoji-koppen)

**Wat je nooit mag doen zonder toestemming:**
- Nieuwe functionele criteria toevoegen die niet (impliciet) in de input staan
- Scope uitbreiden buiten wat de gebruiker aangeeft

---

## Granulariteit

Schrijf zo concreet dat een developer precies weet wat er gebouwd moet worden:
- Benoem echte labelteksten en Button-namen letterlijk, cursief tussen enkele aanhalingstekens (bijv. *'Opslaan'*)
- Vermeld placeholder-teksten letterlijk, cursief tussen enkele aanhalingstekens (bijv. *'Typ een titel'*)
- Geef specifieke waarden waar relevant (max 64 karakters, bij 2 karakters resultaten tonen, etc.)
- Beschrijf tooltip-inhoud als die specifiek is
- Verwijs naar bestaande implementatie met *(conform [X])* zodat developers weten wat ze kunnen hergebruiken

Schrijf niet over technische implementatie (hoe iets gebouwd wordt) — alleen over functioneel gedrag (wat de gebruiker ziet en kan doen).

---

## Somtoday-terminologie

Gebruik altijd de correcte Somtoday-terminologie. De volledige terminologielijst staat in `references/somtoday-terminologie.md` — lees dit bestand bij elke uitwerking.

De meest kritieke regels:

- **Docent** (niet leerkracht), **Leerling** (niet leerder/scholier), **Ouder / verzorger** (niet alleen ouder)
- **Verzenden** (niet versturen) voor officiële acties naar een ontvanger
- **Bewerken** voor inhoudelijke taken, **Wijzigen** voor kleine administratieve ingrepen, **Beheren** voor collecties
- **Annuleren** in formulieren/modals, **Sluiten** voor informatieve schermen, **Terug** in wizards
- **Maken** voor nieuw aanmaken, **Toevoegen** voor bestaand item plaatsen, **Opstellen** voor teksten in concept
- Samenstellingen aaneengeschreven: "leerlingdossier", "absentieregistratie", "roosterwijziging"
- Aanspreken met **je / jij** (nooit "u"), genderneutraal
- Guards: titel beschrijft de actie, Button-teksten bevatten altijd het werkwoord (*'Ja, verwijderen'* — nooit alleen *'Ja'*)

---

## Taal

Schrijf altijd in het **Nederlands**. Gebruik de Somtoday-terminologie uit `references/somtoday-terminologie.md`. Houd technische termen (zoals WYSIWYG, tooltip, guard, toggle, placeholder) in het Engels als dat in de productcontext zo gebruikt wordt.
