# Ticket-stijl (JIRA-klaar)

Bevindingen worden omgezet naar JIRA-klare tickets in de vaste Somtoday/Harmony-handoff-stijl.
Elke 🔴 en 🟠 wordt automatisch een **concept-ticket**. 🟡 en ⚪ komen als **keuzelijst** — de
reviewer bepaalt of daar een ticket van komt.

## Ticketstructuur

Elk ticket bestaat uit precies drie onderdelen:

### 1. Titel
Bondig, benoemt het scherm/de afwijking — niet de techniek. Bijv.
*"Titel op leerlingkaart gebruikt verkeerd kleur-token"*.

### 2. User story
> Als [rol] wil ik [actie/mogelijkheid], zodat [doel/waarde]

Kies de passende rol (docent, leerling, ouder/verzorger, mentor, beheerder, …). Bij een puur
visuele/technische afwijking mag de story de designconsistentie als waarde nemen.

### 3. Acceptatiecriteria
Schrijf vanuit de gebruiker/het gedrag. Neem het **bewijs** concreet op:
- De gemeten of beoordeelde afwijking (design-waarde vs. code-waarde + bron).
- De gewenste eindtoestand (welk token/component/waarde).
- Verwijs naar het reviewpunt en de ernst.

## Opmaakregels (overgenomen uit de handoff-conventie)

- **Vet** voor generieke UI-componentnamen: **Button**, **Input field**, **Checkbox**, **Dropdown**,
  **Radio button**, **Modal**, **Tab**, **Tooltip**, **Toggle** — altijd Engels, ook in NL-tekst.
- *Cursief tussen enkele aanhalingstekens* voor letterlijke labeltekst/melding: *'Opslaan'*.
- `(conform [X])` om naar bestaand gedrag/token te verwijzen.
- Hiërarchische bullets (max 3–4 diep). Emoji-sectiekoppen waar het groepeert.
- Somtoday-terminologie uit `somtoday-terminologie.md` (Docent, Leerling, Ouder/verzorger, Verzenden, …).
- Aanspreken met **je/jij**, genderneutraal.

## Voorbeeld-ticket (uit een 🟠-bevinding)

> **Titel:** Achtergrondkleur van de primaire **Button** wijkt af van het design
>
> **User story:** Als docent wil ik dat knoppen er consistent uitzien, zodat de interface
> herkenbaar en betrouwbaar aanvoelt.
>
> **Acceptatiecriteria**
> - Ik zie dat de primaire **Button** *'Opslaan'* de juiste achtergrondkleur gebruikt.
>   - Gemeten: code `rgb(0, 90, 200)` vs. design-token `color-primary` `rgb(0, 102, 224)` — ΔE2000 = 4,1 (🟠).
>   - Bron: getComputedStyle op `.btn--primary` (`gemeten`, ijk geslaagd).
>   - Gewenst: gebruik het token `color-primary` in plaats van een losse kleurwaarde.

## Koppeling naar het rapport

In het rapport verwijst elke bevinding naar het bijbehorende ticketnummer/-anker en andersom,
zodat een developer van bevinding → ticket → bewijs kan navigeren.
