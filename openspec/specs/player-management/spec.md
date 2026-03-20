### Requirement: Default player roster
The app SHALL initialise with four players named "Player 1", "Player 2", "Player 3", and "Player 4".

#### Scenario: Initial load shows four players
- **WHEN** the page is first loaded
- **THEN** four player entries are displayed in the player management section

### Requirement: Add player
The app SHALL allow the user to add a new player at any time. Each new player SHALL receive a unique default name (e.g. "Player 5").

#### Scenario: Adding a player
- **WHEN** the user clicks the "Add Player" button
- **THEN** a new player entry appears at the bottom of the roster with a default name

### Requirement: Remove player
The app SHALL allow removing a player only when they have no participation in any existing round and the total player count would remain at least 2.

#### Scenario: Removing a player with no round history
- **WHEN** the user clicks the remove control on a player who has not participated in any round AND at least 3 players exist
- **THEN** the player is removed from the roster and all UI

#### Scenario: Removal blocked with round history
- **WHEN** the user attempts to remove a player who participated in at least one round
- **THEN** an inline error is shown and the player is not removed

#### Scenario: Removal blocked at minimum
- **WHEN** only 2 players exist and the user attempts to remove one
- **THEN** an inline error is shown and no player is removed

### Requirement: Rename player
The app SHALL allow the user to rename any player via an editable name field. The new name SHALL propagate immediately to all UI areas: round-entry labels, game-results table headers, summary cards, and special-combo metadata.

#### Scenario: Renaming updates all references
- **WHEN** the user changes a player's name in the player management section and confirms (blur or Enter)
- **THEN** the new name appears in the round-entry grid, the game-results table column header, the summary section, and any special-combo winner labels
