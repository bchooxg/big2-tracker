## ADDED Requirements

### Requirement: Add special combo round
The system SHALL provide an "Add Special Combo" button that creates a fixed-payout round independent of card counts.

#### Scenario: Add special combo with valid active players
- **WHEN** 2–4 players are checked as active and the user clicks "Add Special Combo"
- **THEN** the system presents a winner-selection UI (e.g., a dropdown) listing the active players
- **AND** upon confirmation, the round is recorded with each non-winner paying $3 and the winner receiving $3 × (number of other active players)

#### Scenario: Special combo is balanced
- **WHEN** a special combo round is added
- **THEN** the sum of all active players' scores for that round SHALL be zero

#### Scenario: Insufficient active players for special combo
- **WHEN** fewer than 2 players are checked as active and the user clicks "Add Special Combo"
- **THEN** the system shows an error and does not add the round

#### Scenario: Too many active players for special combo
- **WHEN** more than 4 players are checked as active and the user clicks "Add Special Combo"
- **THEN** the system shows an error and does not add the round

### Requirement: Special combo round display
The system SHALL display special combo rounds in the Game Results table as their own row with distinct visual treatment.

#### Scenario: Special combo row label
- **WHEN** a special combo round is in the results table
- **THEN** the Round column cell shows a "Special Combo" label (in accent color) and optionally the winner's name
- **AND** no card counts are shown for any player cell — only money amounts

#### Scenario: Winner cell highlight
- **WHEN** a special combo round is displayed
- **THEN** the winner's cell is visually highlighted (e.g., "Winner" label, accent color text)

### Requirement: Special combo deletion
The system SHALL allow special combo rounds to be deleted but not edited.

#### Scenario: Delete special combo round
- **WHEN** the user clicks the delete control on a special combo row
- **THEN** that round is removed and all player totals and summaries are recalculated

#### Scenario: No edit control for special combo
- **WHEN** a special combo round is displayed in the results table
- **THEN** no edit control is shown for that row
