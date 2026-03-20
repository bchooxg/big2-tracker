## ADDED Requirements

### Requirement: Edit normal round via modal
The system SHALL allow the user to edit any normal round by clicking an edit control on that round's row, which opens a modal pre-populated with the round's current data.

#### Scenario: Open edit modal
- **WHEN** the user clicks the edit button on a normal round row
- **THEN** a modal opens showing the round's current active player checkboxes and card count inputs

#### Scenario: Save edits recomputes scores
- **WHEN** the user modifies card counts or active player selections and confirms
- **THEN** the round's scores are recomputed using the same pairwise scoring rules
- **AND** the Game Results table, player totals, and session summary are updated

#### Scenario: Edit respects max active player limit
- **WHEN** the user checks more than 4 players in the edit modal and confirms
- **THEN** the system shows an error and does not save the changes

#### Scenario: Edit respects min active player limit
- **WHEN** the user checks fewer than 2 players in the edit modal and confirms
- **THEN** the system shows an error and does not save the changes

#### Scenario: Cancel edit discards changes
- **WHEN** the user closes or cancels the edit modal
- **THEN** the round data remains unchanged

### Requirement: Delete any round
The system SHALL provide a delete control on every round row (normal and special combo) to permanently remove that round.

#### Scenario: Delete a normal round
- **WHEN** the user clicks the delete control on a normal round row
- **THEN** that round is removed from the results table
- **AND** all player totals and session summaries are recalculated

#### Scenario: Delete a special combo round
- **WHEN** the user clicks the delete control on a special combo round row
- **THEN** that round is removed and totals are recalculated
