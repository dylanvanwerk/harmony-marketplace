<!--
  GEBUNDELDE KOPIE — design-review plugin (zelfstandig, Optie C).
  bron:   harmony-foundations skill — Figma file harmony-foundations.ai (key tzrSfWlGdh1O3KOoxQijWk)
  gesynct: 2026-07-10
  versie:  Harmony Foundations token reference (Light/Dark)
  LET OP: dit is een kopie. Bij wijziging in de Harmony-bron moet deze handmatig
  opnieuw gesynct worden (auto-sync valt buiten v1). Dit bestand is bindend voor de
  tokentoets: een hardcoded waarde buiten deze tokens is een bevinding.
-->

# Harmony Foundations — Token Reference

**Figma file:** `harmony-foundations.ai` · key `tzrSfWlGdh1O3KOoxQijWk`

## Architectuur

Twee kleurlagen:
1. **Global color tokens** — ruwe paletten, nooit direct op nodes binden
2. **Semantic color tokens** — altijd gebruiken; verwijzen naar globals; Light + Dark mode

Aanvullend: **Shadows**, **Sizing tokens**, **Typography**

---

## Snel opzoeken — welke token gebruik ik?

| Situatie | Token-categorie |
|---|---|
| Frame/card achtergrond | `bg/{groep}/{sterkte}` |
| Tekst/icoon OP een gekleurde bg token | `fg-on/{zelfde groep}/{zelfde sterkte}` |
| Vrije tekst op neutrale achtergrond | `text/strong` · `text/moderate` · `text/weak` · `text/weakest` |
| Gekleurde tekst (link, badge label) | `fg/{groep}/normal` |
| Rand/stroke | `border/{groep}/{sterkte}` |
| Button / interactief element | `action/{groep}/normal` → hover: `strong` |
| Uitgeschakeld | `disabled/bg` · `disabled/fg` · `disabled/border` |
| Schaduw | `raised/normal` of `raised/strong` + `shadow-color` |
| Gap / padding | `space/{waarde}` |
| Breedte / hoogte | `size/{waarde}` |
| Hoekradius | `border/radius/normal`=6 · `large`=12 · `max`=50 (pill) |

**Kleurgroepen:** `neutral` · `primary`(blauw) · `accent`(geel) · `warning`(oranje) · `negative`(rood) · `positive`(groen) · `alternative`(paars)

**Sterkteschaal:** `weakest` → `weak` → `normal` → `strong` → `strongest` → `max`

---

## 1. Global Color Tokens

Collectie: `Global color tokens` · mode: `Values` · 82 vars · scope: geen (alias-bron only)

| Palet | Stappen | Richting |
|---|---|---|
| `grey` | /0 t/m /150 (16 stappen) | #FFFFFF → #181C20 |
| `blue` | /0 t/m /100 (11 stappen) | lichtblauw → donkermarine |
| `yellow` | /0 t/m /100 | lichtgeel → donkergoud |
| `green` | /0 t/m /100 | lichtgroen → donkergroen |
| `red` | /0 t/m /100 | lichtroze → donkerrood |
| `orange` | /0 t/m /100 | lichtorange → donkerorange |
| `purple` | /0 t/m /100 | lichtpaars → donkerpaars |

**Grijsschaal (meest gebruikt):**

```
grey/0   #FFFFFF    grey/80  #374048
grey/10  #F3F5F6    grey/90  #2E363E
grey/20  #EAEdf0    grey/100 #283139
grey/30  #E2E6E9    grey/110 #2A3137
grey/40  #DADFe3    grey/120 #282E34
grey/50  #D0D6DC    grey/130 #20262D
grey/60  #A7B3BE    grey/140 #1D242A
grey/70  #576275    grey/150 #181C20
```

---

## 2. Semantic Color Tokens

Collectie: `Semantic color tokens` · modes: `Light` / `Dark` · 132 vars

### bg/ — Achtergronden · scope: FRAME_FILL, SHAPE_FILL

| Token | Light | Dark |
|---|---|---|
| `bg/neutral/none` | grey/0 | grey/150 |
| `bg/neutral/weakest` | grey/10 | grey/140 |
| `bg/neutral/weak` | grey/20 | grey/130 |
| `bg/neutral/moderate` | grey/40 | grey/120 |
| `bg/neutral/strong` | grey/60 | grey/100 |
| `bg/neutral/strongest` | grey/70 | grey/60 |
| `bg/neutral/max` | grey/80 | grey/50 |
| `bg/elevated/none` | grey/0 | grey/130 |
| `bg/elevated/weakest` | grey/10 | grey/110 |
| `bg/elevated/weak` | grey/20 | grey/90 |
| `bg/elevated/strong` | grey/30 | grey/80 |
| `bg/primary/weakest` | blue/0 | blue/100 |
| `bg/primary/weak` | blue/10 | blue/90 |
| `bg/primary/normal` | blue/70 | blue/30 |
| `bg/primary/strong` | blue/80 | blue/20 |
| `bg/primary/strongest` | blue/90 | blue/10 |
| `bg/accent/weakest` | yellow/0 | yellow/100 |
| `bg/accent/weak` | yellow/10 | yellow/90 |
| `bg/accent/normal` | yellow/50 | yellow/50 |
| `bg/accent/strong` | yellow/80 | yellow/20 |
| `bg/accent/max` | yellow/90 | yellow/0 |
| `bg/warning/weakest` | orange/0 | orange/100 |
| `bg/warning/weak` | orange/10 | orange/90 |
| `bg/warning/normal` | orange/60 | orange/40 |
| `bg/warning/strong` | orange/80 | orange/10 |
| `bg/warning/max` | orange/90 | orange/0 |
| `bg/negative/weakest` | red/0 | red/100 |
| `bg/negative/weak` | red/10 | red/90 |
| `bg/negative/normal` | red/60 | red/30 |
| `bg/negative/strong` | red/80 | red/10 |
| `bg/negative/max` | red/90 | red/0 |
| `bg/positive/weakest` | green/0 | green/100 |
| `bg/positive/weak` | green/10 | green/90 |
| `bg/positive/normal` | green/80 | green/20 |
| `bg/positive/strong` | green/90 | green/10 |
| `bg/positive/max` | green/100 | green/0 |
| `bg/alternative/weakest` | purple/0 | purple/100 |
| `bg/alternative/weak` | purple/10 | purple/90 |
| `bg/alternative/normal` | purple/50 | purple/20 |
| `bg/alternative/strong` | purple/80 | purple/10 |
| `bg/alternative/max` | purple/90 | purple/0 |
| `bg/mask/normal` | rgba(0,0,0,0.5) | rgba(0,0,0,0.5) |

### fg-on/ — Foreground OP een bg token · scope: ALL_FILLS (+ soms STROKE_COLOR, EFFECT_COLOR)

Gespiegelde naamgeving: `fg-on/primary/normal` gebruik je op `bg/primary/normal`.

| Token | Light | Dark |
|---|---|---|
| `fg-on/neutral/none` | grey/80 | grey/20 |
| `fg-on/neutral/weakest` | grey/80 | grey/20 |
| `fg-on/neutral/weak` | grey/80 | grey/20 |
| `fg-on/neutral/moderate` | grey/80 | grey/20 |
| `fg-on/neutral/strong` | grey/120 | grey/20 |
| `fg-on/neutral/strongest` | grey/0 | grey/150 |
| `fg-on/neutral/max` | grey/0 | grey/150 |
| `fg-on/primary/weakest` | blue/90 | blue/0 |
| `fg-on/primary/weak` | blue/100 | grey/0 |
| `fg-on/primary/normal` | blue/0 | grey/150 |
| `fg-on/primary/strong` | blue/0 | grey/150 |
| `fg-on/primary/strongest` | blue/0 | grey/150 |
| `fg-on/primary/max` | blue/0 | grey/150 |
| `fg-on/accent/weakest` | yellow/90 | yellow/10 |
| `fg-on/accent/weak` | yellow/100 | yellow/0 |
| `fg-on/accent/normal` | grey/150 | grey/150 |
| `fg-on/accent/strong` | grey/150 | grey/150 |
| `fg-on/accent/max` | yellow/0 | grey/120 |
| `fg-on/warning/weakest` | orange/90 | orange/10 |
| `fg-on/warning/weak` | orange/100 | orange/0 |
| `fg-on/warning/normal` | orange/0 | grey/150 |
| `fg-on/warning/strong` | orange/0 | grey/150 |
| `fg-on/warning/max` | orange/0 | grey/120 |
| `fg-on/negative/weakest` | red/90 | red/10 |
| `fg-on/negative/weak` | red/100 | red/0 |
| `fg-on/negative/normal` | red/0 | grey/150 |
| `fg-on/negative/strong` | red/0 | grey/150 |
| `fg-on/negative/max` | red/0 | grey/150 |
| `fg-on/positive/weakest` | green/90 | green/10 |
| `fg-on/positive/weak` | green/100 | green/0 |
| `fg-on/positive/normal` | green/0 | grey/150 |
| `fg-on/positive/strong` | green/0 | grey/150 |
| `fg-on/positive/max` | green/0 | grey/120 |
| `fg-on/alternative/weakest` | purple/90 | purple/10 |
| `fg-on/alternative/weak` | purple/100 | purple/0 |
| `fg-on/alternative/normal` | purple/0 | grey/150 |
| `fg-on/alternative/strong` | purple/0 | grey/150 |
| `fg-on/alternative/max` | purple/0 | grey/120 |

### fg/ — Vrije foreground · scope: ALL_FILLS

| Token | Light | Dark |
|---|---|---|
| `fg/neutral/inverted` | grey/0 | grey/150 |
| `fg/neutral/weak` | grey/30 | grey/70 |
| `fg/neutral/normal` | grey/50 | grey/60 |
| `fg/neutral/moderate` | grey/60 | grey/30 |
| `fg/neutral/strong` | grey/80 | grey/10 |
| `fg/primary/normal` | blue/60 | blue/30 |
| `fg/primary/strongest` | blue/90 | blue/10 |
| `fg/accent/normal` | yellow/60 | yellow/50 |
| `fg/warning/normal` | orange/60 | orange/40 |
| `fg/negative/normal` | red/60 | red/40 |
| `fg/positive/normal` | green/80 | green/20 |
| `fg/alternative/normal` | purple/50 | purple/20 |

### border/ — Randen · scope: STROKE_COLOR

| Token | Light | Dark |
|---|---|---|
| `border/neutral/inverted` | grey/0 | grey/150 |
| `border/neutral/weak` | grey/30 | grey/90 |
| `border/neutral/normal` | grey/50 | grey/80 |
| `border/neutral/strong` | grey/60 | grey/70 |
| `border/neutral/strongest` | grey/70 | grey/60 |
| `border/primary/normal` | blue/70 | blue/20 |
| `border/primary/strong` | blue/80 | blue/40 |
| `border/accent/normal` | yellow/60 | yellow/20 |
| `border/accent/strong` | yellow/80 | yellow/50 |
| `border/warning/normal` | orange/60 | orange/10 |
| `border/warning/strong` | orange/80 | orange/30 |
| `border/negative/normal` | red/60 | red/10 |
| `border/negative/strong` | red/80 | red/30 |
| `border/positive/normal` | green/80 | green/10 |
| `border/positive/strong` | green/90 | green/20 |
| `border/alternative/normal` | purple/50 | purple/10 |
| `border/alternative/strong` | purple/80 | purple/30 |

### text/ — Tekstkleuren · scope: TEXT_FILL

| Token | Light | Dark |
|---|---|---|
| `text/strong` | grey/150 | grey/10 |
| `text/moderate` | grey/80 | grey/30 |
| `text/weak` | grey/70 | grey/60 |
| `text/weakest` | grey/60 | grey/70 |
| `text/inverted` | grey/0 | grey/150 |

Gebruik: `text/strong`=koppen, `text/moderate`=body, `text/weak`=labels, `text/weakest`=placeholders

### action/ — Interactieve elementen · scope: FRAME_FILL, SHAPE_FILL, TEXT_FILL

| Token | Light | Dark |
|---|---|---|
| `action/neutral/weak` | grey/60 | grey/70 |
| `action/neutral/normal` | grey/70 | grey/60 |
| `action/neutral/strong` | grey/80 | grey/10 |
| `action/primary/normal` | blue/60 | blue/30 |
| `action/primary/strong` | blue/80 | blue/40 |
| `action/negative/normal` | red/60 | red/30 |
| `action/negative/strong` | red/80 | red/50 |
| `action/positive/normal` | green/80 | green/20 |
| `action/positive/strong` | green/90 | green/50 |
| `action/warning/normal` | orange/60 | orange/40 |
| `action/warning/strong` | orange/80 | orange/10 |
| `action/accent/normal` | yellow/60 | yellow/20 |
| `action/accent/strong` | yellow/80 | yellow/40 |
| `action/alternative/normal` | purple/50 | purple/20 |
| `action/alternative/strong` | purple/80 | purple/10 |

### disabled/ · scope: ALL_FILLS, STROKE_COLOR

| Token | Light | Dark |
|---|---|---|
| `disabled/bg` | grey/20 | grey/120 |
| `disabled/fg` | grey/60 | grey/70 |
| `disabled/border` | grey/50 | grey/90 |

---

## 3. Shadows

Collectie: `Shadows` · modes: `Light` / `Dark` · 49 vars

**Kleur:** `shadow-color` = grey/150 @ 25% opacity (Light) / 100% opacity (Dark) · scope: EFFECT_COLOR

**Shadow parameters (x / y / blur / spread) — identiek in Light en Dark:**

```
raised/weak:      0,  1,  1, 0    raised/normal:    0,  1,  3, 0
raised/strong:    0,  2,  8, 0    raised/strongest: 0,  2, 12, 0
raised/max:       0,  4, 16, 0

downed/weak:      0, -1,  3, 0    downed/strong:    0, -2,  8, 0
downed/max:       0, -4, 16, 0

centred/weak:     0,  0,  4, 0    centred/normal:   0,  0,  8, 0
left/strong:     -4,  0,  8, 0    right/strong:     3,  0,  8, 0
```

Token-namen per parameter: `{groep}/{sterkte}/x` · `/y` · `/blur` · `/spread` · scope: EFFECT_FLOAT

---

## 4. Sizing Tokens

Collectie: `Sizing tokens` · mode: `Mode 1` · 41 vars

### size/ · scope: WIDTH_HEIGHT
Waarden (px): 0, 1, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 32, 40, 48, 50, 64, 96, 128

### space/ · scope: GAP (aliassen op size/)
Waarden (px): 0, 2, 4, 8, 16, 20, 24, 32, 40, 48, 64, 96, 128

### border/radius/ · scope: CORNER_RADIUS
- `border/radius/normal` = 6px
- `border/radius/large` = 12px
- `border/radius/max` = 50px (pill)

### border/width/ · scope: STROKE_FLOAT
- `border/width/thinnest` = 1px
- `border/width/thin` = 2px

---

## 5. Typography

Collectie: `Typography` · mode: `Mode 1` · 11 vars

| Token | Scope | Waarde |
|---|---|---|
| `family/heading` | FONT_FAMILY | "Open Sans" |
| `family/content` | FONT_FAMILY | "Open Sans" |
| `size/smallest` | FONT_SIZE | 12px |
| `size/small` | FONT_SIZE | 14px |
| `size/normal` | FONT_SIZE | 16px |
| `size/large` | FONT_SIZE | 20px |
| `size/largest` | FONT_SIZE | 26px |
| `weight/regular` | FONT_STYLE | "400" |
| `weight/semi` | FONT_STYLE | "600" |
| `weight/bold` | FONT_STYLE | "700" |
| `height/normal` | LINE_HEIGHT | 140 (140%) |

---

## Bindingsregels

- Altijd **semantische tokens** binden op nodes, nooit globals direct
- Light/Dark mode wisselen via de `Semantic color tokens` collectie-modus
- Scopes zijn leidend: gebruik tokens alleen voor het property-type waarvoor ze bedoeld zijn
- `fg-on/` en `bg/` horen bij elkaar — gebruik altijd het gespiegelde paar voor goede contrast

---

## Gebruik in de tokentoets (design-review)

- Vergelijk gemeten code-kleuren (ΔE2000) met de **semantische** token-waarden hierboven, herleid naar
  de bijbehorende **global** hex (grijsschaal hierboven; overige paletten via de Figma-bron of
  `get_variable_defs`). Een kleur die niet naar een token te herleiden is (losse hex) = bevinding.
- Toets spacing/padding/gap tegen de **`space/`**-waarden en breedtes/hoogtes tegen **`size/`**.
- Toets radius tegen **`border/radius/`** (6 / 12 / 50) en borderbreedte tegen **`border/width/`** (1 / 2).
- Toets font-size tegen **Typography `size/`** (12/14/16/20/26), gewicht tegen **`weight/`** (400/600/700),
  line-height tegen **`height/normal`** (140%), en font-family tegen **Open Sans**.
- Let op **Light vs. Dark**: bepaal eerst welke mode het scherm gebruikt en toets tegen de juiste kolom.

> NB. Alleen de grijsschaal-hexwaarden staan hier expliciet. Voor exacte hex van blue/yellow/green/red/
> orange/purple-stappen: haal ze op via de Figma-bron (`get_variable_defs`) of vul ze hier later aan.
