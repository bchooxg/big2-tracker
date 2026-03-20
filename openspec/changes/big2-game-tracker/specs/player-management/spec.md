## ADDED Requirements

### Requirement: Default player list
The system SHALL initialize with four players named "Player 1", "Player 2", "Player 3", and "Player 4".

#### Scenario: App loads with default players
- **WHEN** the page first loads
- **THEN** four players are displayed in the player list

### Requirement: Add player
The system SHALL allow the user to add a new player at any time.

#### Scenario: Add a new player
- **WHEN** the user clicks "Add Player"
- **THEN** a new player is appended to the list with a default name (e.g., "Player 5")
- **AND** the player appears in round entry checkboxes and in the Game Results table columns

### Requirement: Remove player
The system SHALL allow the user to remove a player, provided at least 2 players remain.

#### Scenario: Remove a player when more than 2 exist
- **WHEN** the user clicks the remove button for a player and 3 or more players exist
- **THEN** the player is removed from the list, from round-entry checkboxes, and from the results table columns

#### Scenario: Attempt to remove when only 2 players remain
- **WHEN** the user clicks the remove button and only 2 players exist
- **THEN** the removal is blocked and an error or disabled state is shown

### Requirement: Rename player
The system SHALL allow the user to rename any player inline.

#### Scenario: Rename a player
- **WHEN** the user edits a player's name field and confirms
- **THEN** the new name is reflected everywhere: round-entry labels, results table headers, summary cards, and any stored special-combo winner metadata

### Requirement: Active player selection per round
The system SHALL display a checkbox next to each player in the Round Entry section so the user can mark which players participate in the upcoming round.

#### Scenario: Select active players
- **WHEN** the user checks 2–4 player checkboxes
- **THEN** only those players are included in round scoring

#### Scenario: Exceed max active players
- **WHEN** the user checks more than 4 player checkboxes and attempts to add a round
- **THEN** the system shows an error message and does not add the round

#### Scenario: Too few active players
- **WHEN** fewer than 2 player checkboxes are checked and the user attempts to add a round
- **THEN** the system shows an error message and does not add the round
