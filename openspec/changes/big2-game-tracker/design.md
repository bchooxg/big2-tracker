## Context

Big 2 Game Tracker is a greenfield single-page application. There is no existing codebase to integrate with. The deliverable is one self-contained `index.html` file that runs locally in any modern browser without a build step or server.

## Goals / Non-Goals

**Goals:**
- Single HTML file with inline CSS and JS — drop-in, zero dependencies
- Correct pairwise Big 2 scoring with card-count multipliers and per-round balance verification
- Dynamic player list: add/remove/rename with live DOM updates
- Special combo rounds with fixed $3 payouts
- Editable normal rounds (card counts + active player toggle) via modal
- Per-round deletion with total recalculation
- Session summary (rounds, biggest winner/loser) and Reset Game

**Non-Goals:**
- Persistence across browser sessions (no localStorage, no backend)
- Multiplayer / network sync
- Export or print functionality
- Mobile-native (PWA, app store)
- Undo/redo history

## Decisions

### Single HTML file
**Decision:** Inline all CSS and JS in one `index.html`.
**Rationale:** The requirement explicitly states "drop into a browser and run." No bundler, no CDN dependency, no file-serving needed.
**Alternative considered:** Separate `.css` / `.js` files — rejected because they require a file server for `import` to work and add deployment friction.

### Pure vanilla JS state model
**Decision:** Maintain a single JS object `state = { players, rounds, pricePerCard }` and re-render the table on every mutation.
**Rationale:** The app is small enough that full re-render is instant and avoids sync bugs between DOM and data. No framework overhead.
**Alternative considered:** Fine-grained DOM patching — more complex, not needed at this scale.

### Scoring algorithm
**Decision:** Compute all pairwise (i, j) payments, accumulate into per-player raw totals, then divide each by 2 to balance.
**Rationale:** Each pair (A→B) is counted twice in the pairwise loop (once as A pays B, once as B pays A), so dividing by 2 yields the correct net. This keeps the loop simple and guarantees ∑ scores = 0.
**Multiplier logic:**
- cards < 10 → 1× (cards × price)
- cards ≥ 10 and < 13 → 2× (cards × price × 2)
- cards = 13 → 3× (cards × price × 3)

### Edit modal for normal rounds
**Decision:** Clicking a round row opens a modal pre-populated with that round's data (active players + card counts). On confirm, recompute scores and re-render.
**Rationale:** Inline editing is complex to implement correctly in a table with dynamic columns. A modal is simpler, less error-prone, and works well on mobile.
**Alternative considered:** Inline editable `<input>` cells — awkward in scrollable tables on mobile.

### Special combo: dropdown winner selection
**Decision:** When "Add Special Combo" is clicked, show a small inline form (within the round-entry panel) with a `<select>` of active players to pick the winner before confirming.
**Rationale:** More discoverable and mobile-friendly than `window.prompt()`.

### Balance check tolerance
**Decision:** If |sum| < 0.001, show ✓ Balanced; otherwise show "Error: $X.XX".
**Rationale:** Floating-point arithmetic can produce tiny non-zero sums (e.g., 1.7763568394e-15). A small epsilon prevents false errors.

## Risks / Trade-offs

- **No persistence** → User loses data on page refresh. Mitigation: out of scope per requirements; could be added with localStorage later.
- **Full re-render on every mutation** → Could flicker or lose scroll position if table is very long. Mitigation: acceptable for typical game sessions (< 50 rounds); scroll position can be preserved by reading `scrollTop` before/after render if needed.
- **Single file gets large** → All logic in one HTML file may grow to 500–800 lines. Mitigation: still manageable; no splitting needed.

## Migration Plan

No migration needed — greenfield. Deployment is placing `index.html` anywhere (local disk, static host, etc.).
