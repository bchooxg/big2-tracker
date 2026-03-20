## ADDED Requirements

### Requirement: Dynamic table columns
The system SHALL maintain a Game Results table with columns: "Round", one column per player (in player-list order), and "Balance Check". The table MUST update whenever players are added, removed, or renamed.

#### Scenario: Player added updates table header
- **WHEN** a new player is added
- **THEN** a new column for that player appears in the Game Results table

#### Scenario: Player removed updates table header
- **WHEN** a player is removed
- **THEN** that player's column is removed from the Game Results table

### Requirement: Round column cell content
The system SHALL display the round identifier and metadata in the Round column cell.

#### Scenario: Normal round label
- **WHEN** a normal round row is rendered and price-per-card is 1
- **THEN** the Round cell shows "Round N" (where N is the 1-based sequential round number)

#### Scenario: Normal round with non-default price
- **WHEN** a normal round row is rendered and price-per-card is not 1
- **THEN** the Round cell shows "Round N" plus a small label like "$X/card"

#### Scenario: Special combo round label
- **WHEN** a special combo round row is rendered
- **THEN** the Round cell shows a "Special Combo" label in accent color, optionally with the winner's name

### Requirement: Normal round player cell content
The system SHALL display card count and money result for each active player in normal round rows.

#### Scenario: Active player cell
- **WHEN** a player was active in a normal round
- **THEN** their cell shows "X cards" on one line and their net money result below it
- **AND** positive amounts are styled green, negative amounts are styled red

#### Scenario: Inactive player cell
- **WHEN** a player was not active in a round
- **THEN** their cell shows "−" in muted color

### Requirement: Special combo player cell content
The system SHALL display only money amounts (no card counts) in special combo round rows.

#### Scenario: Non-winner special combo cell
- **WHEN** a player was active but not the winner in a special combo round
- **THEN** their cell shows their net money result (−$3.00) in red

#### Scenario: Winner special combo cell
- **WHEN** a player was the winner in a special combo round
- **THEN** their cell shows their net money result in green with a "Winner" label in accent color

### Requirement: Horizontal scroll on small screens
The system SHALL make the Game Results table horizontally scrollable on small screens so no data is clipped.

#### Scenario: Table scrolls on narrow viewport
- **WHEN** the viewport is narrower than the table's content width
- **THEN** the table container allows horizontal scrolling without layout breakage
