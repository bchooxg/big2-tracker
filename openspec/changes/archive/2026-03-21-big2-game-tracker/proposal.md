## Why

There is no digital tool for tracking Big 2 card game scores with the specific payout rules used by this group. A dedicated single-file web app eliminates paper scorekeeping errors and automates the complex pairwise payment calculations including card-count multipliers.

## What Changes

- Introduces a brand-new standalone HTML/JS/CSS single-page application (`big2-tracker.html`) with no external dependencies
- Implements configurable per-card pricing with automatic multipliers (2× for 10–12 cards, 3× for 13 cards)
- Implements head-to-head pairwise scoring that always balances to zero per round
- Supports a dynamic player roster (add, remove, rename) with per-round active-player selection (2–4 players)
- Supports "Special Combo" rounds: flat $3/player payout, winner takes all, separate from card-count logic
- Provides a live Game Results table with inline editing, per-round deletion, and balance verification
- Provides a summary section (total rounds, biggest winner, biggest loser) and a Reset Game control

## Capabilities

### New Capabilities

- `player-management`: Add, remove, and rename players; minimum 2 players enforced; names propagate everywhere
- `round-entry`: Per-round price input, active-player checkboxes (2–4), card-count inputs (0–13), and "Add Round" trigger
- `scoring-engine`: Pairwise head-to-head calculation with card-count multipliers and automatic zero-sum balancing
- `special-combo`: Flat $3-per-loser special round entry with winner selection, balanced payout, table display
- `game-results-table`: Dynamic table with per-player columns, card counts, money results, balance check column, edit/delete controls
- `round-editing`: Click-to-edit modal for normal rounds allowing card count and participation changes with score recomputation
- `summary-display`: Running totals, biggest winner/loser cards, and Reset Game button

### Modified Capabilities

<!-- none — this is a greenfield app -->

## Impact

- New file: `big2-tracker.html` (single self-contained deliverable)
- No existing code, APIs, or dependencies affected
- Pure client-side; no backend, no build step, no external libraries
