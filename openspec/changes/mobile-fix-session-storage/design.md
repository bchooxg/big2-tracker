## Context

`index.html` is a single self-contained HTML file. When a round is added, the results table renders with `white-space: nowrap` and multiple player columns. On mobile the table width can exceed the viewport, causing the browser to scale the entire page down (viewport zoom-out) instead of triggering the `overflow-x: auto` scroll on the wrapper. Session storage persistence is entirely absent — state lives only in memory.

## Goals / Non-Goals

**Goals:**
- Prevent page-level zoom-out on mobile when the results table appears
- Keep all table overflow contained within `.table-wrapper` so the rest of the page stays at normal zoom
- Persist `state.players` and `state.rounds` to `sessionStorage` after every mutation
- Restore state from `sessionStorage` on page load before the first `render()`
- Clear `sessionStorage` when Reset Game is confirmed

**Non-Goals:**
- `localStorage` persistence across closed tabs (session only, as requested)
- Server-side or cloud sync
- Versioned migration of stored state schema

## Decisions

### 1. Root cause of mobile zoom-out: table min-width fighting the viewport
**Decision:** The table has `white-space: nowrap` and no explicit max-width constraint on the wrapper. When the table renders, its natural width can exceed `100vw`. The browser then scales the page to fit — this overrides the viewport meta tag behaviour in some mobile browsers. Fix by adding `max-width: 100%` to `.table-wrapper` and ensuring `table-layout: auto` with `min-width` only on individual cells (not the table itself forcing extra width).

Additionally, set `width: max-content` on the `<table>` so it sizes to its content but the wrapper clips and scrolls it — the page itself never needs to resize.

**Alternative considered:** `table-layout: fixed` — rejected because column widths become hard to control without knowing player name lengths.

### 2. Session storage: JSON serialise the entire state object
**Decision:** After every `render()` call, serialize `state` with `JSON.stringify` and write to `sessionStorage` under the key `'big2-state'`. On load, attempt `JSON.parse(sessionStorage.getItem('big2-state'))` and merge into `state` if valid; also restore `_nextPlayerId` and `_nextRoundId` from the maximum IDs found in the restored data to avoid ID collisions.

**Rationale:** Simple, no schema migration needed for a single-session tool. The entire state is small (< 10 KB for typical game sessions).

**Alternative considered:** Only persisting `rounds` — rejected because player names would be lost on refresh.

### 3. Restore counter IDs from stored data
**Decision:** After restoring state, set `_nextPlayerId = Math.max(...players.map(p => p.id)) + 1` and `_nextRoundId = Math.max(...rounds.map(r => r.id)) + 1` (with safe fallbacks for empty arrays). This prevents new players/rounds from reusing existing IDs.

### 4. Reset Game clears session storage
**Decision:** In `resetGame()`, after clearing `state.rounds`, also call `sessionStorage.removeItem('big2-state')` (or re-save the cleared state, which is equivalent). The players roster is preserved in session storage since Reset Game keeps players.

### 5. No UI indicator needed
**Decision:** Avoid adding a banner or toast — it adds complexity for minimal benefit. The behaviour (state survives refresh) is self-evident once working.

## Risks / Trade-offs

- **Corrupted sessionStorage** → Wrap restore in try/catch; fall back to default state silently on any parse error.
- **ID collision after restore** → Mitigated by Decision 3.
- **Mobile zoom fix may not work on all browsers** → The `max-width:100%` + `overflow-x:auto` approach is the standard pattern and works on Chrome/Safari/Firefox mobile. Adding `display: block` to `.table-wrapper` (making it a block formatting context) ensures the scroll container is established correctly.
