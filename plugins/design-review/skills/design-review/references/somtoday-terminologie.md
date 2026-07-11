<!--
  GEBUNDELDE KOPIE — design-review plugin (zelfstandig, Optie C).
  bron:   harmony-os/skills/4-handoff-acceptatie-criteria/references/somtoday-terminologie.md
  gesynct: 2026-07-10
  LET OP: dit is een kopie. Bij wijziging in de harmony-os-bron moet deze
  handmatig opnieuw gesynct worden (auto-sync valt buiten v1).
-->

# Somtoday-terminologie voor acceptatiecriteria

Gebruik deze terminologie consequent in alle acceptatiecriteria. De correcte term staat links; wat je moet vermijden staat rechts.

---

## Rollen en personen

| Gebruik | Vermijd |
|---|---|
| Docent | Leerkracht, leraar (in UI-teksten) |
| Leerling | Leerder, scholier |
| Mentor | Klassenleraar |
| Schoolleiding | Directeur (tenzij letterlijk die persoon bedoeld wordt) |
| Beheerder | Admin, administrator (in gebruikersgerichte teksten) |
| Ouder / verzorger | Alleen "ouder" als ook verzorgers de doelgroep zijn |

---

## Onderwijs en roostering

| Gebruik | Vermijd |
|---|---|
| Rooster | Schema, agenda (als het over lessen gaat) |
| Lesuur | Uur, periode |
| Vak | Course, subject |
| Schooljaar | Jaar (alleen als context volledig helder is) |
| Studiewijzer | Planner, lesplanner |
| Lesitem | Les, lesonderdeel |
| Jaarbijlagen | Jaarmateriaal, documenten |
| Onderwijssoort | Schooltype, niveau — gebruik bij voorkeur de specifieke aanduiding: vmbo-b, vmbo-k, vmbo-t, vmbo-gl, havo, vwo |

---

## Toetsing en resultaten

| Gebruik | Vermijd |
|---|---|
| Toets | Proefwerk (in formele UI-teksten) |
| Cijfer | Score, beoordeling (tenzij het aantoonbaar geen cijfer is) |
| Rapport | Rapportage (voor leerlingrapport) |
| Toetsdossier | Cijferlijst (als het over het hele dossier gaat) |
| Voortgangsdossier | Voortgangsrapport |
| SE (schoolexamen) | Schooltoets |
| CE (centraal examen) | Landelijk examen |
| Weging | Gewicht, zwaarte |

---

## Absentie en zorg

| Gebruik | Vermijd |
|---|---|
| Absentie | Verzuim (voor dagelijkse registratie in de UI) |
| Ongeoorloofd verzuim | Spijbelen (in UI-teksten) |
| Zorgvierkant | Zorgmodule |
| Signaleringslijst | Aandachtslijst |
| Registratie | Notitie (als het een officiële registratie betreft) |

---

## Modulenamen (altijd met hoofdletter als eigennaam)

Studiewijzer, Toetsdossier, Voortgangsdossier, Examendossier, Zorgvierkant, Signaleringslijst, Notitieboek, Leermiddelen, Jaarbijlagen

---

## Samenstellingen (aaneengeschreven, geen spatie)

leerlingdossier, roosterwijziging, absentieregistratie, cijferlijst, toetsdossier, schoolexamen, studiewijzer, lesitem, jaarbijlagen, leerlinggegevens, voortgangsdossier, signaleringslijst, onderwijssoort, pakketkeuze

---

## Werkwoorden voor acties (Buttons en AC-beschrijvingen)

**Verzenden vs. Versturen**
- Gebruik **verzenden** voor officiële, definitieve acties richting een ontvanger.
- Gebruik **versturen** nooit in UI-teksten of AC.

**Tonen / Bekijken / Weergeven**
- **Bekijken** — de gebruiker navigeert proactief naar informatie (leidt naar nieuwe pagina).
- **Tonen** — de interface voert een directe opdracht uit op de huidige pagina (toggles, resultaten tonen). Actie van het systeem.
- **Weergeven** — uitsluitend voor de manier waarop inhoud gepresenteerd wordt ("lijstweergave").

**Bewerken / Wijzigen / Beheren**
- **Beheren** — organisatorische taak over een collectie (volgorde, toegang, toevoegen/verwijderen).
- **Wijzigen** — kleine, administratieve ingreep (naam of status wijzigen).
- **Bewerken** — inhoudelijke of creatieve taak aan bestaand materiaal.

**Annuleren / Sluiten / Terug**
- **Annuleren** — in een modal of formulier als de gebruiker de actie wil afbreken. Bij wijzigingen: altijd een guard.
- **Sluiten** — voor informatieve schermen (sidebar, informatievenster).
- **Terug** — navigatie door stappen in een wizard/proces.

**Toevoegen / Maken / Opstellen**
- **Maken** — compleet nieuw item creëren.
- **Toevoegen** — bestaand item ergens bij plaatsen.
- **Opstellen** — specifiek voor teksten in conceptfase die nog verzonden/gepubliceerd worden.

**Publiceren vs. Opslaan**
- **Opslaan** — individuele opslag zonder melding aan derden.
- **Publiceren** — statuswijziging van concept naar zichtbaar voor doelgroep. Altijd nevenoptie "Opslaan als concept" aanbieden.

---

## Guards (bevestigingsdialogen)

Structuur van een guard in de AC:

- Titel: beschrijft de actie direct — bijv. *"Wil je de wijzigingen weggooien?"*
- Body: concreet wat er verloren gaat — bijv. *"De inleveringen van 24 leerlingen gaan verloren."*
- Primaire (destructieve) Button: kort + werkwoord — bijv. *'Ja, verwijderen'*
- Secundaire Button: *'Nee, annuleren'* of *'Nee, doorgaan met bewerken'*

Vermijd "Weet je zeker dat…" als guardtitel.
Vermijd Buttons met alleen *'Ja'* of *'Nee'* — altijd contextueel label.

---

## Aanspreekvorm

- Altijd **je** of **jij** (nooit "u").
- Genderneutraal: "de docent", "de leerling" — geen hij/zij.
- **Mijn** voor titels van onderdelen waarvan de gebruiker eigenaar is: "Mijn rooster", "Mijn notitie".
- **Je / jouw** als de interface helpt of de weg wijst: "Je docent heeft je inleveropdracht nagekeken."

---

## UI-componenten (altijd Engels)

Generieke UI-componentnamen schrijf je altijd in het Engels, ook in Nederlandse lopende tekst — dit sluit aan bij de benaming in code. De labeltekst óp het component (bijv. wat er op een Button staat) blijft Nederlands.

| Gebruik | Vermijd |
|---|---|
| Button | Knop |
| Input field | Invoerveld, tekstveld |
| Checkbox | Aanvinkvakje |
| Radio button | Keuzerondje |
| Dropdown | Keuzelijst, uitklaplijst |
| Modal | Venster, popup |
| Tab | Tabblad |
| Tooltip | (al Engels — ongewijzigd) |
| Placeholder | (al Engels — ongewijzigd) |
| Toggle | Schakelaar |

---

## Productnamen (vaste schrijfwijze)

- "Somtoday" — niet "SomToday" of "SOMTODAY"
- "Harmony" — niet "harmony" in lopende tekst
- LAS, BRON, OSO, BRP, BRIN, DUO — altijd afkorting, altijd hoofdletters
- SE (schoolexamen), CE (centraal examen) — altijd afkorting
