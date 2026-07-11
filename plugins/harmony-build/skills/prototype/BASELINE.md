# BASELINE — ingebouwde design-minimumlat

Dit is de **terugvaloptie** achter het design-slot (zie `SKILL.md`). Zodra de
`Somtoday-Frontend-Design`-skill beschikbaar is, laadt die en neemt 'ie deze
regels over. Tot dan gelden onderstaande minima. Hou het minimaal: dit is geen
volledige design-filosofie, alleen genoeg om slop te voorkomen.

## Grayscale-discipline
- Grijstinten dragen de hiërarchie; blauw alleen voor **dé** primaire actie,
  focus, en één subtiel accent per scherm. Nooit blauw als versiering.
- Eén `.btn--primary` per scherm. Meer primaire acties = onduidelijke taak.

## Hiërarchie & inhoud
- Elk scherm heeft één duidelijke **kern-taak** die visueel bovenaan/centraal staat.
- Échte NL-content: echte vaknamen, echte knoplabels, plausibele data. Geen
  lorem ipsum, geen "Knop 1 / Knop 2".
- Toon voor leerling & ouder: **B1-taal** — korte zinnen, geen jargon, actief.
  Voor docent & medewerker mag vakterminologie, maar blijf helder.

## Anti-AI-slop (verboden denkwijzen)
- **Geen generiek dashboard** als niemand erom vroeg. Bouw de gevraagde taak,
  niet "een overzicht met kaartjes en KPI's".
- **Geen decoratieve iconensoep, gradients, emoji-koppen, hero-secties** die
  niets met de taak te maken hebben.
- **Geen verzonnen features** buiten scope. Buiten-scope = zichtbaar-maar-`data-dead`.
- **Geen symmetrie-om-de-symmetrie**: vul geen lege plek met een tweede kaartje
  puur voor de balans. Leegte mag.
- Kopieer geen "modern SaaS landing page"-reflex. Dit is een intern schoolsysteem-
  scherm voor een concrete taak.

## Toegankelijkheid (minimum)
- Touch-targets ≥ 44px op mobiel. Zichtbare focus (zit in `kit.css`).
- Labels aan inputs. Klikbare dingen zijn `<button>`/`<a>`, geen kale `<div>`.

> Bij twijfel over "is dit goed design volgens Somtoday": dat oordeel hoort
> straks in `Somtoday-Frontend-Design`. Deze baseline stelt alleen de ondergrens.
