## 1. Fix Modal Centering

- [x] 1.1 Add `position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%); margin: 0` to the `dialog` CSS rule
- [x] 1.2 Set `max-height: 90vh; overflow-y: auto` on `dialog` so tall modals scroll internally on small screens
- [x] 1.3 Verify both the Special Combo modal and Edit Round modal open centred at narrow (375px) and wide (1280px) viewports

## 2. Refined Design Tokens

- [x] 2.1 Expand `:root` tokens: add `--shadow-sm`, `--shadow-md`, `--shadow-lg`, `--radius-sm`, `--radius-lg`, `--accent-dark` (hover shade), `--surface-hover`
- [x] 2.2 Update header to use a gradient background (`--accent` → `--accent-dark`) for depth
- [x] 2.3 Replace flat card `box-shadow` with `--shadow-md`; use `--shadow-lg` on modals

## 3. Button Polish

- [x] 3.1 Set `min-height: 38px` on all `.btn` for touch-target compliance
- [x] 3.2 Add `transition: background-color .15s, box-shadow .15s, transform .1s` to `.btn`
- [x] 3.3 Add `:active` state: `transform: scale(0.97)` for tactile feedback
- [x] 3.4 Add `:focus-visible` outline using accent colour for keyboard accessibility
- [x] 3.5 Darken `.btn-primary` and `.btn-accent` backgrounds on `:hover` using `--accent-dark`

## 4. Card & Section Polish

- [x] 4.1 Increase card `padding` to `1.5rem` and `border-radius` to `12px`
- [x] 4.2 Add subtle `border-top: 3px solid var(--accent)` on `.card h2` to create section identity
- [x] 4.3 Style the `<header>` with gradient and increase vertical padding; add a subtle text shadow on the title

## 5. Mobile-First Layout

- [x] 5.1 Make `.player-grid` default to 1 column on mobile, 2 columns at `min-width: 480px`, auto-fill at `min-width: 700px`
- [x] 5.2 Make `.entry-actions` and `.entry-controls` flex-wrap and full-width buttons on mobile (`width: 100%` below 480px)
- [x] 5.3 Make `.summary-grid` 1 column on mobile, auto-fit at `min-width: 480px`
- [x] 5.4 Ensure `.player-row` inputs are full-width and readable on 375px (no truncation)
- [x] 5.5 Set `font-size: 1rem` on all `input` and `select` elements to prevent iOS auto-zoom on focus

## 6. Sticky First Column in Results Table

- [x] 6.1 Add `position: sticky; left: 0; z-index: 2; background: var(--surface2)` to `th:first-child` in the results table
- [x] 6.2 Add `position: sticky; left: 0; z-index: 1; background: var(--surface2)` to `td.round-label` and `td:first-child` in the totals row
- [x] 6.3 Add a subtle right `box-shadow` on sticky cells to indicate they are pinned: `box-shadow: 2px 0 4px rgba(0,0,0,.06)`

## 7. Table & Cell Readability

- [x] 7.1 Add `min-width` to player columns (`min-width: 90px`) so narrow card counts don't squish
- [x] 7.2 Add alternating row background (`tbody tr:nth-child(even)`) using `--surface` for scanability
- [x] 7.3 Increase table cell padding slightly to `.6rem .85rem` for breathing room
- [x] 7.4 Style the totals footer row with a stronger border-top and bolder background

## 8. Modal Polish

- [x] 8.1 Add `border-radius: var(--radius-lg)` and `--shadow-lg` to dialogs
- [x] 8.2 Add a header bar inside each modal with an accent left-border or coloured title
- [x] 8.3 Style modal action buttons to be full-width stacked on mobile (`flex-direction: column-reverse` below 400px)
- [x] 8.4 Add `backdrop-filter: blur(2px)` to `dialog::backdrop` for depth effect
