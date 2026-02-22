# Spell Effects Database

## Source

- **API:** [5e SRD API](https://www.dnd5eapi.co/api/2014/spells) by [5e-bits](https://github.com/5e-bits/5e-srd-api)
- **License:** Open Game License (OGL) v1.0a (SRD content)
- **Date fetched:** 2026-02-21
- **Total spells:** 319 (full 2014 SRD)

## Files

| File | Shipped? | Description |
|------|----------|-------------|
| `spell-effects.json` | ✅ Yes | Compact runtime lookup (28KB). Spell name → effect notes, conditions, flags. |
| `dev-data/srd-spells-raw.json` | ❌ No (gitignored) | Full parsed data with all fields for development. |
| `dev-data/srd-spell-slugs.json` | ❌ No | API slug list for re-fetching. |

## How `spell-effects.json` is used

The app loads it on startup and uses it as the primary source for:
- **Effect notes** in the combat log (e.g. "DEX save or outlined: attacks have ADV, can't be invisible")
- **Buff bar tooltips** on hover
- **Condition detection** (frightened, charmed, blinded, etc.)

Falls back to description-based keyword parsing for homebrew/non-SRD spells.

## How to update

1. Re-fetch from the API (see `dev-data/README.md` for scripts)
2. Review/update `effect_notes` in `srd-spells-raw.json`
3. Rebuild `spell-effects.json` with the compact export script
4. Commit and push

## Notes

- Covers 2014 PHB spells only. 2024 PHB spell updates may differ.
- D&D Beyond may use different spell names than SRD. Non-matching spells use fallback parsing.
