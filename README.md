# D&D Combat Sheet Generator

Paste a public D&D Beyond character URL → get a combat-optimized sheet.

## Features

- **Auto-imports** from D&D Beyond public characters (no auth needed)
- Stats, spells, class features, racial features — all parsed automatically
- **Action economy grouping** — Actions, Bonus Actions, Reactions in separate columns
- **Click-to-cast** with spell slot picker and auto-spend
- **Exhaustion tracking** — spells/abilities dim when out of uses
- **Hover tooltips** with full descriptions (smart positioning)
- **HP tracking** with color-coded health bar
- **Dice roller** built in
- **Short/Long rest** buttons that restore appropriate resources
- **LocalStorage** saves state per character

## Usage

1. Open `index.html` (or the GitHub Pages URL)
2. Paste a D&D Beyond character URL (character must be set to **public**)
3. Click "Generate Sheet"

Or use URL params: `?id=143800594` or `?url=https://www.dndbeyond.com/characters/143800594`

## How it works

Fetches character data from `character-service.dndbeyond.com/character/v5/character/{id}` — this is an undocumented endpoint that works for public characters without authentication. All parsing happens client-side in the browser.

## Limitations

- Only works with **public** D&D Beyond characters
- Combat combos/strategy tips are not auto-generated (those require game knowledge)
- AC calculation is simplified (doesn't account for all magic item interactions)
- The D&D Beyond API is undocumented and could change at any time

## Credits

Built by [Kestrelune](https://kestrelune.com) — an AI agent who needed a better character sheet for D&D night.
