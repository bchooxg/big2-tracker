### Requirement: Table structure
The Game Results table SHALL have a "Round" column, one column per player in roster order, and a "Balance Check" column.

#### Scenario: Player columns match roster
- **WHEN** the game results table is rendered
- **THEN** there is one column header per player, in the same order as the player roster

### Requirement: Round column label
Each row's Round cell SHALL display "Round N" (sequential 1-based count across all round types). For normal rounds with a price other than $1, a secondary label "$X/card" SHALL appear beneath "Round N". For special combo rounds, a "Special Combo" label (and optionally winner name) SHALL appear.

#### Scenario: Normal round at default price shows no price label
- **WHEN** a normal round is added at $1/card
- **THEN** the Round cell shows "Round N" with no price annotation

#### Scenario: Normal round at custom price shows price label
- **WHEN** a normal round is added at $2/card
- **THEN** the Round cell shows "Round N" and "$2/card" beneath it

#### Scenario: Special combo round label
- **WHEN** a special combo round row is rendered
- **THEN** the Round cell shows "Round N" and "Special Combo" (with winner name)

### Requirement: Normal round player cells
For a normal round, each active player's cell SHALL display the card count on one line and the monetary result below it (with a "+" prefix for positive values). Positive values SHALL be styled green, negative red, zero neutral. Inactive players SHALL show "-" in muted styling.

#### Scenario: Active player shows cards and money
- **WHEN** a player is active in a normal round
- **THEN** their cell shows "X cards" and their monetary result with colour coding

#### Scenario: Inactive player shows dash
- **WHEN** a player is not active in a round
- **THEN** their cell displays "-" in a muted colour

### Requirement: Balance Check column
Each row's Balance Check cell SHALL compute the sum of all player scores for that round. If the absolute value is less than $0.01, it SHALL display "✓ Balanced" in muted text. Otherwise it SHALL display "Error: $X.XX" in red.

#### Scenario: Balanced round shows checkmark
- **WHEN** a round's player scores sum to within $0.01 of zero
- **THEN** the Balance Check cell shows "✓ Balanced"

#### Scenario: Unbalanced round shows error
- **WHEN** a round's player scores do not sum to zero (beyond $0.01 tolerance)
- **THEN** the Balance Check cell shows "Error: $X.XX" in red

### Requirement: Horizontal scroll on small screens
The game results table wrapper SHALL allow horizontal scrolling when the table content is wider than the viewport. The first column (Round label) SHALL be sticky so it remains visible while scrolling horizontally.

#### Scenario: Table scrollable on narrow viewport
- **WHEN** the viewport is narrow enough that the table overflows
- **THEN** the table container scrolls horizontally without breaking the page layout

#### Scenario: Round column stays visible while scrolling
- **WHEN** the user scrolls the results table horizontally
- **THEN** the Round column remains fixed in place and visible at all times
