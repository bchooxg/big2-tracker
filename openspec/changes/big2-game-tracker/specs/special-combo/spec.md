## ADDED Requirements

### Requirement: Special Combo entry
The app SHALL provide an "Add Special Combo" button that creates a special round type not tied to card counts. The same active-player selection (2–4 players) from the round-entry section SHALL apply.

#### Scenario: Button triggers special combo flow
- **WHEN** the user clicks "Add Special Combo"
- **THEN** a modal or inline UI appears for selecting the winner among currently active players

#### Scenario: Active player validation applies
- **WHEN** fewer than 2 or more than 4 players are active and the user clicks "Add Special Combo"
- **THEN** an error is shown and the modal does not open

### Requirement: Special Combo payout calculation
Each non-winner active player SHALL pay exactly $3. The winner SHALL receive $3 × (number of non-winner active players). The round MUST sum to zero.

#### Scenario: Three-player special combo payout
- **WHEN** 3 players are active and Player A is selected as winner
- **THEN** Player A receives +$6, Player B pays -$3, Player C pays -$3, sum = $0

#### Scenario: Four-player special combo payout
- **WHEN** 4 players are active and Player A is winner
- **THEN** Player A receives +$9, others each pay -$3, sum = $0

### Requirement: Special Combo winner selection
The app SHALL present a dropdown (select element) pre-populated with the names of currently active players for the user to choose the winner.

#### Scenario: Dropdown contains active players only
- **WHEN** the special combo modal opens
- **THEN** the winner dropdown lists exactly the currently active players and no others

### Requirement: Special Combo appearance in results table
Special Combo rounds SHALL appear as their own row in the Game Results table with a visible "Special Combo" label in the Round column, the winner's name indicated, and only monetary values (no card counts) in player cells. The winner's cell SHALL be visually highlighted.

#### Scenario: Special Combo row shows monetary values only
- **WHEN** a special combo round exists in the results table
- **THEN** each active player's cell shows only a dollar amount (no "X cards" line)

#### Scenario: Winner cell is highlighted
- **WHEN** a special combo round row is rendered
- **THEN** the winner's cell displays a "Winner" indicator in the primary accent colour

### Requirement: Special Combo deletion
Special Combo rounds SHALL be deletable via the same per-row delete control as normal rounds. They SHALL NOT be editable.

#### Scenario: Delete removes special combo row
- **WHEN** the user clicks delete on a special combo row
- **THEN** the row is removed and all totals and summaries are recalculated

#### Scenario: No edit control on special combo rows
- **WHEN** a special combo row is rendered
- **THEN** no edit button or inline editing control is visible
