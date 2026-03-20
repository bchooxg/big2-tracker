## Context

This is a greenfield single-page application with no existing codebase to integrate with. The deliverable is one self-contained HTML file with inline CSS and JavaScript. The app must work by opening the file directly in a browser (file:// protocol) with zero build steps or server requirements.

## Goals / Non-Goals

**Goals:**
- Single `big2-tracker.html` file that opens in any modern browser with no installation
- Correct zero-sum pairwise scoring with card-count multipliers
- Dynamic player roster (add/remove/rename) that propagates everywhere reactively
- Per-round active player selection (2–4), card-count inputs, and "Add Round" flow
- Special Combo round type: flat $3/loser, balanced, winner highlighted
- Editable normal rounds (card counts + participation) via modal; delete any round
- Game Results table with balance-check column; summary cards; Reset Game

**Non-Goals:**
- Persistence across browser sessions (no localStorage, no backend)
- Multi-device sync or sharing
- Support for Big 2 variants with different scoring rules
- Undo/redo history beyond simple round deletion

## Decisions

### 1. Single HTML file with inline CSS and JS
**Decision:** All code lives in one `.html` file — `<style>` block for CSS, `<script>` block for JS.
**Rationale:** The explicit requirement. Maximizes portability; no bundler, no npm, no server needed.
**Alternative considered:** Separate files with a simple dev server — rejected because it adds setup friction.

### 2. Vanilla JS state object + full re-render on change
**Decision:** Maintain a plain JS object (`state = { players, rounds }`) and call a single `render()` function after every mutation.
**Rationale:** Keeps logic simple and avoids framework weight. For a page of this size, full DOM re-render is imperceptible.
**Alternative considered:** Fine-grained DOM patching — adds complexity with no meaningful benefit at this scale.

### 3. Scoring algorithm: pairwise then halve
**Decision:** For N active players, compute all N*(N-1)/2 head-to-head pairs. Each pair produces a raw transfer (loser pays winner loser_cards × price × multiplier). Sum each player's raw balance, then divide all by 2.
**Rationale:** Halving is required to avoid double-counting since each pair contributes to both players' running totals. The result is a perfectly zero-sum round.
**Multiplier rules:** cards 10–12 → 2×; cards 13 → 3×; otherwise 1×.

### 4. Card-count multiplier applies to the loser's card count only
**Decision:** When player A (fewer cards) beats player B (more cards), the multiplier is determined by B's card count, and B pays A: `B.cards × price × multiplier(B.cards)`.
**Rationale:** Standard Big 2 house rules as specified.

### 5. Edit modal for normal rounds
**Decision:** Clicking a round row (or an edit button) opens a `<dialog>` element pre-populated with current card counts and active-player checkboxes. On save, recompute that round's scores and re-render.
**Rationale:** `<dialog>` is native, accessible, no library needed. Inline cell editing would be cramped on mobile.
**Alternative considered:** Inline `contenteditable` cells — harder to validate and recompute atomically.

### 6. Special Combo via dropdown in a modal
**Decision:** Clicking "Add Special Combo" opens a small modal with a `<select>` pre-populated with active players to pick the winner. No money input needed.
**Rationale:** Cleaner UX than a browser `prompt()`; keeps all UI in-page.

### 7. Player renaming via inline editable name fields in the player management section
**Decision:** Each player row has a text input for their name. Changes propagate to all round metadata (stored by player index/id, not name string) and re-render.
**Rationale:** Rounds store player references by a stable ID (array index at creation time or a UUID), so renaming never corrupts history.

### 8. CSS-only responsive layout, no framework
**Decision:** Use CSS Grid and Flexbox for layout; `overflow-x: auto` on the results table wrapper for mobile scroll.
**Rationale:** Requirement explicitly states CSS only, no frameworks.

## Risks / Trade-offs

- **Floating-point precision** → Use `Math.round(x * 100) / 100` (2 decimal places) throughout; balance check uses `< 0.01` tolerance.
- **No persistence** → Refreshing the page loses all data. Acceptable per non-goals, but worth a visible warning or future enhancement note.
- **Player removal with existing rounds** → Removing a player who participated in past rounds could leave orphaned data. Mitigation: mark removed players as "inactive" in the roster but keep their column in historical rounds; alternatively, disallow removal if they have round history and show an error.
- **Table width on mobile** → Many players × many columns can overflow. Mitigation: `overflow-x: auto` wrapper on the table.
- **Max 4 active players per round** → Enforced by validation before adding the round; error message shown inline.

## Migration Plan

N/A — greenfield file. Deployment is simply placing `big2-tracker.html` anywhere accessible (local filesystem, static host, etc.).

## Open Questions

- Should player removal be blocked if they have round history, or should historical rounds show a "removed" placeholder? (Recommendation: block removal and show an error — simpler and safer.)
- Should the app offer a "Save to file" / export feature in a future iteration? (Out of scope for now.)
