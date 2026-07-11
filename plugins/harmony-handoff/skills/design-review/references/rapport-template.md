# Rapport-template

Het rapport is Markdown, geschreven **vanuit de stem van een Designer** die developers
constructieve, feitelijke feedback geeft. Eén rapport per sessie; het aggregeert alle
review-eenheden met een samenvatting bovenaan. Opslaan als `rapport.md` in de aparte werkmap.

Vul de template letterlijk in; laat lege secties niet weg maar meld "n.v.t." met reden.

---

```markdown
# Design Review — <feature/scherm> — <datum>

## Samenvatting
- **Overall oordeel:** <Akkoord | Akkoord met kanttekeningen | Aanpassingen nodig | Afgekeurd>
- **Review-eenheden:** <aantal>
- **Bevindingen:** 🔴 <n> · 🟠 <n> · 🟡 <n> · ⚪ <n>
- **Kern in één zin:** <wat een developer als eerste moet weten>

## Dekking & beperkingen
- **Brontype:** <Figma-URL | Figma-prototype | Claude Design prototype>
- **Meet-ijk (`DR.selftest`):** <geslaagd | gefaald: welke checks>
- **Tokenversie:** <uit kop harmony-foundations.md> — <gevuld | nog leeg>
- **Gemeten:** <welke reviewpunten> · **Beoordeeld:** <…> · **Niet toetsbaar:** <… + reden>
- **Viewports gereviewd:** <bv. 1280px desktop, 375px mobiel>
- **Zelfcontrole-loop:** uitgevoerd — <n> bevindingen na verificatie gedowngraded/verwijderd.

---

## Eenheid 1 — <framenaam ↔ schermstaat>
- **Design:** <Figma-URL / prototype-URL>  ·  **Code:** <staging-route>
- **Oordeel:** <…>
- **Bewijs:** `design.png` ↔ `code.png` (naast elkaar), meetwaarden hieronder.

### Bevindingen

#### 🔴/🟠/🟡/⚪ [<categorie>] <korte titel>
- **Label:** <gemeten | beoordeeld/handmatig>
- **Bewijs:** design = <waarde/bron> · code = <waarde/bron> · <ΔE / contrast / px>
- **Aanbeveling:** <welk token/component/waarde>
- **Ticket:** <#anker of "keuzelijst">

#### Meetwaarden (tabel)
| Element | Eigenschap | Design | Code | Token | Δ / oordeel |
|---|---|---|---|---|---|
| .card__title | font-size | 20px | 18px | text-l (20px) | −2px 🟡 |
| .btn--primary | background | #0066E0 | #005AC8 | color-primary | ΔE 4,1 🟠 |
| .card__label | contrast | — | 3,9:1 | — | < 4,5:1 🔴 |

### Nog te verifiëren door mens (⚪)
- <hover-gedrag, animatie, screenreader, responsief detail…>

---

## Eenheid 2 — <…>
<zelfde structuur>

---

## JIRA-klare tickets

> Concept-tickets uit 🔴/🟠. Voor 🟡/⚪ zie de keuzelijst eronder.

### Ticket 1 — <titel>
<user story + acceptatiecriteria conform ticket-stijl.md>

### Ticket 2 — <titel>
<…>

### Keuzelijst (🟡/⚪ — reviewer beslist of hier een ticket van komt)
- [ ] <bevinding> — <korte reden>
- [ ] <bevinding> — <korte reden>
```
