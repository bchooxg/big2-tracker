## 1. HTML Skeleton & CSS Foundation

- [x] 1.1 Create `big2-tracker.html` with DOCTYPE, `<head>` (meta charset, viewport, title), empty `<style>` and `<script>` blocks
- [x] 1.2 Write CSS custom properties (colour tokens: green, red, accent, muted, neutral, surface, border)
- [x] 1.3 Write base CSS: reset, body font, layout containers (header, main sections, footer)
- [x] 1.4 Write responsive CSS: flexbox/grid for section layout; `overflow-x: auto` table wrapper for mobile

## 2. State Model & Core Data Structures

- [x] 2.1 Define JS `state` object: `{ players: [{id, name}], rounds: [] }`
- [x] 2.2 Define round shape for normal rounds: `{ id, type:'normal', pricePerCard, participants:[{playerId, cards, score}] }`
- [x] 2.3 Define round shape for special-combo rounds: `{ id, type:'special', participants:[{playerId, score}], winnerId }`
- [x] 2.4 Write `render()` dispatcher that calls all section renderers on every state mutation

## 3. Player Management Section

- [x] 3.1 Build `renderPlayerManagement()`: outputs player list with name `<input>` and remove button per player, plus "Add Player" button
- [x] 3.2 Implement "Add Player": appends new player with default name, calls `render()`
- [x] 3.3 Implement rename: on `input` blur/Enter update player name in state, call `render()`
- [x] 3.4 Implement remove player: validate ≥2 players and no round participation; show inline error or remove + `render()`

## 4. Round Entry Section

- [x] 4.1 Build `renderRoundEntry()`: outputs price-per-card input, player grid (checkbox + card-count input per player), "Add Round" and "Add Special Combo" buttons
- [x] 4.2 Implement "Add Round" click: collect active players, validate count (2–4) and card counts (0–13), call scoring engine, push round to state, reset inputs, `render()`
- [x] 4.3 Implement inline validation error display for round entry (player count and card count errors)

## 5. Scoring Engine

- [x] 5.1 Write `getMultiplier(cards)`: returns 3 for 13, 2 for 10–12, 1 otherwise
- [x] 5.2 Write `computeRoundScores(participants, pricePerCard)`: iterate all pairs, compute raw transfers, sum per player, halve all, round to 2 dp; return `[{playerId, score}]`
- [x] 5.3 Write unit-style inline tests (console assertions) to verify: 2-player round sums to zero, 3-player round sums to zero, multipliers correct at 9/10/13 cards

## 6. Special Combo Flow

- [x] 6.1 Implement "Add Special Combo" click: validate active player count (2–4), open winner-selection modal
- [x] 6.2 Build winner-selection `<dialog>`: `<select>` of active player names, Confirm and Cancel buttons
- [x] 6.3 On Confirm: compute special combo scores ($3 per loser, winner gets 3×losers), push round to state, close modal, `render()`

## 7. Game Results Table

- [x] 7.1 Build `renderResultsTable()`: construct `<table>` with header row (Round, one th per player, Balance Check)
- [x] 7.2 Render normal round rows: Round cell with label and optional price annotation; per-player cells with "X cards" + coloured money amount or "-"; Balance Check cell
- [x] 7.3 Render special combo round rows: Round cell with "Special Combo" + winner name; per-player cells with money only; winner cell highlighted with "Winner" label
- [x] 7.4 Implement Balance Check cell logic: sum scores, compare to 0.01 threshold, render "✓ Balanced" or "Error: $X.XX"
- [x] 7.5 Add delete button to each row: on click remove round from state, `render()`
- [x] 7.6 Add edit button to normal round rows only (no edit on special combo)

## 8. Round Editing Modal

- [x] 8.1 Build edit `<dialog>`: pre-populate with round's pricePerCard, active-player checkboxes, card-count inputs
- [x] 8.2 On Save: validate inputs (2–4 active, card counts 0–13); show inline modal errors on failure
- [x] 8.3 On Save success: update round in state with new values, recompute scores via scoring engine, call `render()`
- [x] 8.4 On Cancel: close modal with no state changes

## 9. Summary Section

- [x] 9.1 Build `renderSummary()`: compute cumulative per-player totals from all rounds; find biggest winner and biggest loser
- [x] 9.2 Render "Total Rounds" card (count of all rounds)
- [x] 9.3 Render "Biggest Winner" card (name + "+$X.XX") and "Biggest Loser" card (name + "-$X.XX"); show "-" when no rounds
- [x] 9.4 Implement "Reset Game" button: on click (with confirmation), clear `state.rounds`, `render()`

## 10. Styling Polish & UX

- [x] 10.1 Apply colour coding: green for positive amounts, red for negative, neutral for zero throughout table and summary
- [x] 10.2 Style special-combo labels in primary accent colour; style winner cell highlight
- [x] 10.3 Style modals (`<dialog>`): backdrop, padding, button layout, close on backdrop click
- [x] 10.4 Ensure responsive layout: test at 375px width (mobile) and 1280px (desktop); confirm table scrolls horizontally
- [x] 10.5 Final cross-browser check: open in Chrome, Firefox, Safari/Edge; verify no console errors
