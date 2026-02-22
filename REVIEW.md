# Code Review & Reflection — Feb 22, 2026

## What we built (Saturday session)
Single-file D&D 5e combat sheet pulling from D&D Beyond API. ~2500 lines of vanilla JS/HTML/CSS in one file. No framework, no build step. GitHub Pages hosted.

## Honest assessment

### What's good
- **It works.** Three real characters load, render, and play correctly.
- **The API parsing is thorough.** Handles 2014/2024 PHB, multiclass, item spells, weapon mastery, expertise, domain spells.
- **Smart combat log.** Dice breakdowns, effect notes, condition tags — teaches the rules while you play.
- **141 SRD magic items + 319 spell effects** loaded as JSON. Data-driven, not hardcoded per-spell.

### What needs refactoring
- **The file is too big.** 2500+ lines of inline JS. `buildSheet()` alone is ~400 lines. Should split into modules (parser, renderer, combat engine, data layer).
- **Feature detection is a growing allowlist.** `passiveFeatures` array will keep growing. Need a generic "is this a passive" check from the API data (activation type, no action cost, etc.).
- **State management is scattered.** `window._char`, `window._hp`, `window._spellData`, `window._featureData`, `window._itemData` — global soup. One state object.
- **`useFeature()` is a 200-line switch statement.** Each class feature is a special case. Should be data-driven: feature → effect template → resolution.
- **`autoCast()` is similarly monolithic.** Damage, healing, saves, attacks, buffs all in one function with nested ifs.
- **CSS is inline in `<style>`.** Works but hard to maintain. Could be a separate file.
- **No tests.** Parser logic is complex enough to warrant unit tests (spell parsing, damage calculation, template resolution).
- **`sv()`/`ld()` save/load is fragile.** Queries DOM by class names. If rendering changes, persistence breaks silently.

### What's missing (features)
- **Concentration tracking.** Casting a CONC spell should warn/drop the existing one.
- **Death saves.** No UI for tracking them.
- **Multiclass spell slot calculation.** Currently uses first class only — multiclass casters need the combined table.
- **Warlock Pact Magic.** Short rest slots at fixed level, separate from regular slots.
- **Conditions on self.** Can't mark yourself as prone, grappled, etc.
- **Mobile layout.** Three columns don't work on phones. Need responsive breakpoints.
- **Undo.** Misclick a spell slot? Too bad. Need undo or at least confirm for expensive actions.

### Architecture direction
If this grows further, the right move is:
1. Split into `parser.js` (API → character model), `renderer.js` (model → HTML), `engine.js` (combat logic), `state.js` (persistence).
2. Character model as a clean object, not DOM-coupled.
3. Event-driven: click → engine processes → state updates → renderer patches DOM.
4. Tests on parser and engine (node-runnable, no DOM needed).

But honestly? For a single-file tool that three people use at a D&D table, the current architecture is *fine*. Refactor when it hurts, not before.

## Meta: How to make reflection happen

This file should be read by future-me at the start of any dnd-combat-sheet session. Add to AGENTS.md or session startup: "If working on dnd-combat-sheet, read REVIEW.md first."

After each significant session, append a new reflection section. Keep it honest. Delete stale observations.
