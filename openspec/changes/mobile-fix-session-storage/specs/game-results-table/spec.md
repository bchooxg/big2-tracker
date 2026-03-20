## MODIFIED Requirements

### Requirement: Horizontal scroll on small screens
The game results table wrapper SHALL allow horizontal scrolling when the table content is wider than the viewport. The wrapper SHALL be established as a block formatting context (`display: block`) with `max-width: 100%` and `overflow-x: auto` so that the table's natural width is clipped and scrolled within the wrapper — it MUST NOT cause the browser to zoom out the entire page on mobile. The first column (Round label) SHALL be sticky so it remains visible while scrolling horizontally.

#### Scenario: Table scrollable on narrow viewport
- **WHEN** the viewport is narrow enough that the table overflows
- **THEN** the table container scrolls horizontally without breaking the page layout

#### Scenario: No page zoom-out on mobile when table appears
- **WHEN** a round is added and the results table becomes visible on a mobile viewport
- **THEN** the page does not scale down or zoom out; only the table wrapper scrolls internally

#### Scenario: Round column stays visible while scrolling
- **WHEN** the user scrolls the results table horizontally
- **THEN** the Round column remains fixed in place and visible at all times
