## 1. Fix Mobile Table Zoom-Out

- [x] 1.1 Add `display: block; max-width: 100%` to `.table-wrapper` CSS rule to establish a block formatting context that clips table overflow
- [x] 1.2 Change `table` CSS: replace any fixed `width: 100%` with `width: max-content; min-width: 100%` so the table sizes to its content but never forces the page wider than the viewport
- [x] 1.3 Verify `.table-wrapper` already has `overflow-x: auto` and `-webkit-overflow-scrolling: touch`; add if missing

## 2. Session Storage — Save

- [x] 2.1 Write a `saveState()` function that calls `sessionStorage.setItem('big2-state', JSON.stringify(state))`
- [x] 2.2 Call `saveState()` at the end of `render()` so every mutation is automatically persisted
- [x] 2.3 Ensure `resetGame()` calls `sessionStorage.removeItem('big2-state')` (or re-saves after clearing rounds) so reset is persisted

## 3. Session Storage — Restore on Load

- [x] 3.1 Write a `loadState()` function that wraps `sessionStorage.getItem` + `JSON.parse` in a try/catch; return `null` on any error
- [x] 3.2 In `loadState()`, if valid data is found: overwrite `state.players` and `state.rounds`, then recalculate `_nextPlayerId` as `Math.max(0, ...state.players.map(p => p.id)) + 1` and `_nextRoundId` as `Math.max(0, ...state.rounds.map(r => r.id)) + 1`
- [x] 3.3 Call `loadState()` before the initial `render()` call at the bottom of the script; if it returns `null` leave the default state untouched
