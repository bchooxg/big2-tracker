## MODIFIED Requirements

### Requirement: Horizontal scroll on small screens
The game results table wrapper SHALL allow horizontal scrolling when the table content is wider than the viewport. The first column (Round label) SHALL be sticky so it remains visible while scrolling horizontally.

#### Scenario: Table scrollable on narrow viewport
- **WHEN** the viewport is narrow enough that the table overflows
- **THEN** the table container scrolls horizontally without breaking the page layout

#### Scenario: Round column stays visible while scrolling
- **WHEN** the user scrolls the results table horizontally
- **THEN** the Round column remains fixed in place and visible at all times
