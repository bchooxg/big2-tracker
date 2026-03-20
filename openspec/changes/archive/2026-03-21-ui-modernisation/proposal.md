## Why

The current UI feels dated, has layout issues on mobile devices, and modals (Special Combo / Edit Round) appear in the top-left corner of the page instead of being centred — making them awkward to use on any screen size.

## What Changes

- Redesign visual style: modern card shadows, refined typography, consistent spacing, polished colour palette, subtle hover/focus states
- Fix modal centering: `<dialog>` elements must be positioned in the centre of the viewport on all screen sizes
- Improve mobile layout: stack sections vertically, use full-width inputs, make the player grid and results table touch-friendly, ensure tap targets meet minimum size
- Improve results table readability on small screens: sticky first column, horizontal scroll, compact cell layout
- Add visual polish: smooth transitions on buttons and modals, improved focus rings for accessibility

## Capabilities

### New Capabilities

<!-- none — all changes are improvements to existing UI behaviour -->

### Modified Capabilities

- `game-results-table`: Table must remain horizontally scrollable and readable on viewports as narrow as 375px; first column (Round) should be sticky
- `round-editing`: Edit modal must be centred in the viewport and usable on mobile
- `special-combo`: Special Combo modal must be centred in the viewport and usable on mobile

## Impact

- `big2-tracker.html` — CSS and HTML structure changes only; no JS logic changes
- No external dependencies added; remains a single self-contained file
