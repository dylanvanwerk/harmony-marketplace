---
description: Start een Design Review — vergelijk een gebouwde PR/staging (of Claude Design prototype) met het design en genereer een NL-rapport met JIRA-klare tickets.
---

Start een **Design Review**. Volg de skill `design-review` (in deze plugin) en haar fasen.

Argumenten (optioneel, mag de gebruiker ook tijdens de intake aanleveren): $ARGUMENTS

Ga zo te werk:

1. Laad en volg de `design-review`-skill en haar referenties.
2. **Fase 0 — Intake:** bepaal de **design-bron-URL** (Figma-URL / Figma-prototype / Claude Design
   prototype) en de **PR/staging-URL**. Detecteer het brontype en bevestig het. Benoem meteen de
   verwachte dekking (wat wel/niet toetsbaar is bij deze bron).
3. Check de randvoorwaarden vroeg:
   - Is de **Figma MCP** geautoriseerd (alleen nodig bij een Figma-bron)? Zo niet: meld het en werk
     met de Claude-Design-prototype-bron of een aangeleverde screenshot-export.
   - Is er een **verbonden, ingelogde Chrome** (Chrome-MCP) met het scherm klaargezet?
4. Vraag welke **review-eenheden** (frame ↔ schermstaat) en welke **viewport(s)** meegaan, en maak
   de werkmap `design-review/<datum>-<eenheid>/` aan.
5. Doorloop de fasen (Chrome verbinden → koppelen → meten+ijk → beoordelen → zelfcontrole → rapport+tickets),
   met een korte bevestiging per fase.

Houd de kernprincipes aan: harde scheiding **gemeten** vs. **beoordeeld**, "geen bewijs, geen bevinding",
ijk vóór meting, reviewer bevestigt de koppeling, en de zelfcontrole-loop vóór het rapport.
