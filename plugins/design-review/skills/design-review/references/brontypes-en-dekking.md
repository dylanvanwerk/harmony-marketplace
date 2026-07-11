# Brontypes & dekking

De plugin detecteert het brontype van het design en past de reviewset + rapportdekking aan.
De dekking wordt **altijd expliciet** in het rapport benoemd: wat kon wel/niet getoetst worden en waarom.

## Detectie

| Signaal | Brontype |
|---|---|
| URL bevat `figma.com/design`, `figma.com/file`, of een `node-id` | **Figma-URL** (frame/component) |
| URL bevat `figma.com/proto` | **Figma-prototype** |
| Een Claude Design prototype / gehoste HTML-URL (geen figma.com) | **Claude Design prototype** |

Vraag bij twijfel de reviewer om het brontype te bevestigen.

## Wat is toetsbaar per bron

| Reviewpunt | Figma-URL | Figma-prototype | Claude Design prototype |
|---|---|---|---|
| Kleur vs. **Harmony-token** via `get_variable_defs` | ✅ echte tokens | ⚠️ deels | ❌ geen Figma-tokens |
| Kleur-**ΔE2000** design vs. code | ✅ (uit design-context/screenshot) | ✅ (screenshot) | ✅ DOM-vs-DOM |
| Typografie & spacing (design-zijde) | ✅ metadata/design-context | ⚠️ beperkt | ✅ getComputedStyle op design-DOM |
| Contrast (WCAG) | ✅ op code-zijde | ✅ op code-zijde | ✅ beide zijden |
| Componentnaam/variant/state | ✅ via metadata | ⚠️ deels | ⚠️ uit DOM-structuur (beoordeeld) |
| Visuele gelijkenis (screenshot) | ✅ | ✅ | ✅ |

## Gevolgen per bron

### Figma-URL (volledige tokentoets)
- Haal tokens op met `get_variable_defs`, metadata met `get_metadata`, referentiebeeld met `get_screenshot`,
  en indien nodig `get_design_context`.
- Vergelijk gemeten code-kleuren (ΔE2000) tegen de Figma-token-waarden én tegen de gebundelde
  `harmony-foundations.md`.
- **Vereist dat de Figma MCP geautoriseerd is.** Zo niet → meld dit en behandel als niet-toetsbaar (⚪),
  of val terug op screenshot-vergelijking als de reviewer een export aanlevert.

### Figma-prototype
- Als Figma-URL, maar de token-uitlezing is beperkt/afhankelijk van het geselecteerde frame.
- Benoem expliciet welke frames wel/niet uitleesbaar waren.

### Claude Design prototype (DOM-vs-DOM)
- Er zijn **geen Figma-tokens**. Open het prototype in Chrome (of tweede tab), meet met dezelfde
  meetscripts (Script 1–4) → je vergelijkt **design-DOM vs. code-DOM**.
- Toets beide zijden bovendien tegen de gebundelde `harmony-foundations.md`.
- Rapportnotitie (verplicht): *"Figma-tokentoets n.v.t. — getoetst tegen Harmony-foundations en design-DOM."*

## Rapport: sectie "Dekking & beperkingen"

Neem in elk rapport op:
- Welk brontype gedetecteerd is.
- Welke reviewpunten **gemeten**, welke **beoordeeld**, en welke **niet toetsbaar** waren (+ reden).
- Of de meet-ijk (`DR.selftest()`) is geslaagd; zo niet, welke metingen daardoor vervielen.
- Welke tokenversie is gebruikt (uit de kop van `harmony-foundations.md`), en of dat bestand gevuld was.
- Openstaande ⚪ handmatige checks.
