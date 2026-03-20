## ADDED Requirements

### Requirement: Edit control on normal rounds
Each normal round row in the Game Results table SHALL have an edit button. Special combo rows SHALL NOT have an edit button.

#### Scenario: Edit button present on normal rounds
- **WHEN** a normal round row is rendered
- **THEN** an edit button is visible in that row

#### Scenario: No edit button on special combo rows
- **WHEN** a special combo round row is rendered
- **THEN** no edit button is present

### Requirement: Edit modal opens with current values
Clicking the edit button on a normal round SHALL open a modal pre-populated with that round's current card counts and active-player checkboxes. The price-per-card for that round SHALL also be editable.

#### Scenario: Modal pre-populated
- **WHEN** the user clicks edit on a round
- **THEN** a modal opens showing each player's current card count and active/inactive status for that round

### Requirement: Edit saves and recomputes
Clicking "Save" in the edit modal SHALL update the round's stored data, recompute the round's scores using the standard scoring rules, and update all per-player totals and summaries.

#### Scenario: Save updates round data
- **WHEN** the user changes a card count and clicks Save
- **THEN** the game results table reflects the new card count and the recomputed monetary values for that round

#### Scenario: Totals and summary update after edit
- **WHEN** a round is edited and saved
- **THEN** the per-player cumulative totals and biggest winner/loser summary cards reflect the updated values

### Requirement: Edit validation
The edit modal SHALL enforce the same rules as initial round entry: 2–4 active players and card counts 0–13.

#### Scenario: Edit rejected with invalid card count
- **WHEN** the user enters a card count outside 0–13 in the edit modal and clicks Save
- **THEN** an error is shown and the round is not updated

#### Scenario: Edit rejected with wrong player count
- **WHEN** fewer than 2 or more than 4 players are checked in the edit modal and Save is clicked
- **THEN** an error is shown and the round is not updated

### Requirement: Delete round
Every round row (normal and special combo) SHALL have a delete control. Clicking it SHALL remove the round from storage and trigger a full recalculation of all totals and summaries.

#### Scenario: Delete removes row and updates totals
- **WHEN** the user clicks delete on any round row
- **THEN** the row disappears from the table and all cumulative totals and summary cards update to reflect the remaining rounds
