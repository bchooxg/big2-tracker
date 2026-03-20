## Context

`big2-tracker.html` is a single self-contained HTML file with inline `<style>` and `<script>` blocks. The current CSS uses basic custom properties and flexbox/grid, but lacks polish: flat button styles, no transitions, minimal spacing hierarchy, and crucially — `<dialog>` elements are not explicitly positioned, causing browsers to render them at the top of the document flow rather than centred in the viewport.

## Goals / Non-Goals

**Goals:**
- Centre `<dialog>` modals in the viewport on all screen sizes (fix the top-left bug)
- Polish visual design: improved shadows, rounded corners, refined colour usage, better button hierarchy
- Improve mobile usability: larger tap targets, single-column stacking, readable table on 375px viewports
- Sticky first column in the results table so player context is always visible when scrolling horizontally
- Smooth micro-interactions: button hover/active states, modal open transition

**Non-Goals:**
- Changing any JS logic, scoring, or data model
- Adding CSS frameworks or external dependencies
- Dark mode
- Animations that could distract during score entry

## Decisions

### 1. Fix `<dialog>` centering with explicit CSS
**Decision:** Add explicit CSS to force `dialog` elements to be centred:
```css
dialog {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  margin: 0;
}
```
**Rationale:** The HTML `<dialog>` spec leaves default positioning to the browser; Chrome/Edge render it near the top of the scrollable document rather than the viewport centre. Explicit `position: fixed` with transform centering is the reliable cross-browser fix.
**Alternative considered:** `margin: auto` — works in some browsers but not reliably when the page is scrolled.

### 2. Mobile-first CSS rewrite of layout sections
**Decision:** Rewrite section layouts as mobile-first (single column base, grid enhancements at `min-width: 600px`).
**Rationale:** The current layout works on desktop but stacks poorly on small screens. Mobile-first avoids override clutter.

### 3. Sticky first column in results table
**Decision:** Apply `position: sticky; left: 0; z-index: 1; background: inherit` to the first `td`/`th` in every table row.
**Rationale:** With many players the table scrolls horizontally; without a sticky round label the user loses context. Pure CSS, no JS required.

### 4. Refined design tokens (CSS custom properties)
**Decision:** Expand the existing `--` token set with surface gradients, a shadow scale (`--shadow-sm`, `--shadow-md`, `--shadow-lg`), and a primary gradient for the header. Keep all values in `:root` for easy future theming.
**Rationale:** Centralised tokens make the visual language consistent without duplicating values.

### 5. Button hierarchy via visual weight
**Decision:** Three button tiers — primary (filled accent), secondary (outlined), destructive (red filled). All buttons get `min-height: 38px` for touch target compliance.
**Rationale:** Current buttons are all similar weight; adding hierarchy guides the user's eye to the intended action.

## Risks / Trade-offs

- **`position: fixed` on `<dialog>` ignores scroll** → Desired behaviour: modal always visible regardless of scroll position. This is correct.
- **Sticky column in table requires `overflow-x: auto` on a *direct* wrapper** → The sticky cell needs the scrolling ancestor to be the immediate wrapper div, not `body`. Current structure already uses `.table-wrapper`; just needs `overflow-x: auto` confirmed.
- **Visual rewrite could mask existing content** → Keep all existing IDs and class names that JS references intact; only add or rename presentational classes.

## Migration Plan

All changes are confined to the `<style>` block and HTML structure of `big2-tracker.html`. No data migration or deployment steps needed beyond replacing the file.
