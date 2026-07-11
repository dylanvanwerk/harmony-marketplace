# Interactie-checklist

Interactiegedrag toetsen we in twee lagen: een **vaste Harmony-basislijst** (altijd) plus
**scherm-specifieke aanvullingen** (afgeleid uit de aanwezige componenten). Meet automatisch
waar het kan (Chrome-MCP, Script 5); markeer de rest als ⚪ handmatig.

## Vaste Harmony-basislijst (elk scherm)

| Check | Automatiseerbaar? | Hoe |
|---|---|---|
| Elk interactief element heeft een zichtbare **focus-state** | ✅ deels | Script 5a per interactief element |
| Logische **tab-volgorde** (DOM-volgorde = leesvolgorde) | ✅ | Script 5b + reviewer beoordeelt volgorde |
| Alle interactieve elementen **toetsenbord-bereikbaar** (geen keyboard-trap) | ✅ deels | Script 5b (staan ze in de lijst?) |
| **Hover**-feedback op klikbare elementen (desktop) | ❌ | ⚪ handmatig |
| Gedrag klopt op de gekozen **viewport(s)** (responsief) | ✅ | Script 5d: resize + hermeten |
| Zichtbare **states**: default / hover / active / focus / disabled aanwezig zoals in design | ⚠️ deels | meten waar kan, anders ⚪ |
| **Animaties/transities** vloeiend en conform design | ❌ | ⚪ handmatig |

## Scherm-specifieke aanvulling (voorbeelden)

Leid extra checks af uit de aanwezige Harmony-componenten:

- **Modal** aanwezig → Esc sluit (Script 5c), focus-trap binnen modal, focus keert terug bij sluiten (⚪).
- **Dropdown / Select** → openen/sluiten met toetsenbord, pijltjes navigeren opties (⚪ deels).
- **Input field / formulier** → validatie-/foutstates, focus-volgorde, verplicht-markering (meten waar kan).
- **Tabs** → pijltjestoetsen wisselen tab, actieve tab zichtbaar (⚪ deels).
- **Toggle / Checkbox / Radio** → schakelt met spatie/enter, state zichtbaar (meten waar kan).
- **Tooltip** → verschijnt bij focus én hover, verdwijnt met Esc (⚪ deels).

## Resultaat

Elke interactie-check wordt een bevinding met label `gemeten` (Script 5) of `beoordeeld/handmatig` (⚪).
Openstaande ⚪ checks komen in het rapport onder *"Nog te verifiëren door mens"*.
