## 1. Project Scaffold

- [ ] 1.1 Create `index.html` with full HTML5 boilerplate (doctype, head, meta viewport, title)
- [ ] 1.2 Add CSS reset and CSS custom properties (color palette: green, red, accent, muted)
- [ ] 1.3 Define responsive layout skeleton: header, two-column panel (round entry + player list), results section, summary section

## 2. State Model

- [ ] 2.1 Define JS `state` object: `{ players: [], rounds: [], nextRoundNumber: 1 }`
- [ ] 2.2 Initialize state with 4 default players (id, name, total)
- [ ] 2.3 Implement `render()` dispatcher that re-renders player list, round-entry grid, results table, and summary after every mutation

## 3. Player Management

- [ ] 3.1 Render player list with inline rename input and remove button per player
- [ ] 3.2 Implement "Add Player" button — appends new player, calls render()
- [ ] 3.3 Implement remove player — blocks if ≤ 2 players remain, else removes and calls render()
- [ ] 3.4 Implement rename player — updates player name in state and re-renders everywhere (table headers, entry labels, summary)

## 4. Round Entry UI

- [ ] 4.1 Render Round Entry section: price-per-card input (min 0.1, step 0.1, default 1)
- [ ] 4.2 Render player grid: checkbox (active) + card count input (0–13) per player
- [ ] 4.3 Wire active-player checkboxes to enable/disable corresponding card count inputs

## 5. Scoring Engine

- [ ] 5.1 Implement `computeRoundScores(activePlayers, cardCounts, pricePerCard)` — pairwise loop, multiplier logic, divide-by-2 balancing
- [ ] 5.2 Write unit-style inline tests (console.assert) to verify: 2-player, 4-player, 13-card (3×), 10-card (2×) cases
- [ ] 5.3 Implement `validateRoundBalance(scores)` — returns true if |sum| < 0.001

## 6. Add Round

- [ ] 6.1 Implement "Add Round" button handler — validate active player count (2–4), validate card counts (0–13), call scoring engine, push round to state, re-render, reset inputs to 0
- [ ] 6.2 Show inline error messages for validation failures (active count, card count range)

## 7. Special Combo

- [ ] 7.1 Render "Add Special Combo" button and inline winner-selection `<select>` (populated from active players)
- [ ] 7.2 Implement special combo handler — validate active count (2–4), compute scores (non-winners: −$3, winner: +$3 × others), push round to state, re-render
- [ ] 7.3 Show error if active player count is invalid for special combo

## 8. Game Results Table

- [ ] 8.1 Render table with dynamic columns (Round + one per player + Balance Check)
- [ ] 8.2 Render normal round rows: Round cell (label + price tag if ≠ $1), active player cells (cards + money, color-coded), inactive player cells ("−"), Balance Check cell
- [ ] 8.3 Render special combo round rows: Round cell (Special Combo label + winner name), player cells (money only, winner highlighted), Balance Check cell
- [ ] 8.4 Make table container horizontally scrollable (`overflow-x: auto`)

## 9. Round Editing

- [ ] 9.1 Add edit button to each normal round row (no edit button for special combo rows)
- [ ] 9.2 Build edit modal HTML: active-player checkboxes + card count inputs, pre-populated from round data
- [ ] 9.3 Implement modal open/close logic (show/hide, populate fields)
- [ ] 9.4 Implement modal save — validate active count (2–4) and card counts (0–13), recompute scores, update round in state, re-render

## 10. Round Deletion

- [ ] 10.1 Add delete button to every round row
- [ ] 10.2 Implement delete handler — remove round from state, recalculate sequential round numbers, update player totals, re-render

## 11. Session Summary

- [ ] 11.1 Render summary cards below table: Total Rounds, Biggest Winner (name + amount), Biggest Loser (name + amount)
- [ ] 11.2 Compute cumulative player totals from all rounds on every render
- [ ] 11.3 Implement "Reset Game" button — confirm prompt, clear rounds, zero player totals, re-render

## 12. Polish & Responsive Styling

- [ ] 12.1 Apply color coding: positive amounts green, negative red, zero neutral; special-combo accent color
- [ ] 12.2 Style summary cards, player list panel, and round-entry panel for desktop layout
- [ ] 12.3 Add responsive breakpoints so layout stacks vertically on mobile
- [ ] 12.4 Style edit modal overlay (backdrop, centered card, close button)
- [ ] 12.5 Final pass: verify all edge cases (0-card winner, all same card count, single active pair)
