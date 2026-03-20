## Why

Big 2 (Big Two) is a popular card game often played for money, but tracking scores across multiple rounds—especially with variable card counts, multipliers, and special combos—is tedious and error-prone with pen and paper. A dedicated web app eliminates calculation mistakes and provides a clear, persistent record of each session.

## What Changes

- Introduce a new standalone single-page web application: `index.html`
- No existing code is modified; this is a greenfield feature

### New Features
- Dynamic player management (add, remove, rename; 2–unlimited players)
- Per-round active player selection (2–4 players per round)
- Configurable price-per-card (default $1)
- Pairwise head-to-head scoring with card-count multipliers (2× for 10–12 cards, 3× for 13 cards)
- Special combo rounds: fixed $3/player payout, no card counts
- Live Game Results table with balance validation per round
- Inline editing of normal rounds and per-round deletion
- Session summary: total rounds, biggest winner, biggest loser
- Reset Game to clear rounds while preserving player list

## Capabilities

### New Capabilities
- `player-management`: Add, remove, and rename players; manage active-player selection per round
- `round-scoring`: Head-to-head pairwise scoring with configurable price and card-count multipliers; balance verification
- `special-combo`: Fixed-payout special combo rounds with winner selection
- `game-results-table`: Dynamic results table showing card counts, money results, balance check per round
- `round-editing`: Edit card counts / active players on existing normal rounds; delete any round
- `session-summary`: Aggregated totals, biggest winner/loser display, reset game action

### Modified Capabilities
<!-- none — greenfield project -->

## Impact

- New file: `index.html` (self-contained; inline CSS + JS, no external dependencies)
- No backend, no build step, no frameworks required
- Works in any modern browser
