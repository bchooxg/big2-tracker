### Requirement: Price per card input
The Round Entry section SHALL include a numeric input for "Price per Card ($)" with a minimum of 0.1, a step of 0.1, and a default value of 1.

#### Scenario: Default price is $1
- **WHEN** the page loads
- **THEN** the price-per-card input shows 1.00

#### Scenario: Price change is applied to next round
- **WHEN** the user changes the price input before clicking "Add Round"
- **THEN** the new round uses the updated price per card in all calculations

### Requirement: Active player selection
Each player in the roster SHALL appear in the round-entry grid with a checkbox labelled with their name. Only players whose checkbox is checked are "active" for that round.

#### Scenario: All players shown with checkboxes
- **WHEN** the round-entry section is rendered
- **THEN** every player in the roster has a checkbox and a card-count input

#### Scenario: Unchecked player is excluded
- **WHEN** a player's checkbox is unchecked and the user adds a round
- **THEN** that player is not included in the round's scoring

### Requirement: Card count input per active player
Each player row in the round-entry grid SHALL include a numeric card-count input (0–13, integer). The input SHALL only be relevant when the player's checkbox is checked.

#### Scenario: Valid card count accepted
- **WHEN** a checked player's card-count input is an integer between 0 and 13 inclusive
- **THEN** the round is accepted for that player's count

#### Scenario: Invalid card count rejected
- **WHEN** any checked player's card-count input is outside 0–13 or non-integer
- **THEN** the round is not added and an inline error is shown

### Requirement: Active player count validation
The app SHALL enforce that exactly 2, 3, or 4 players are active for any normal round. Fewer than 2 or more than 4 active players MUST prevent round submission.

#### Scenario: Too few active players
- **WHEN** fewer than 2 players are checked and "Add Round" is clicked
- **THEN** an error message is shown and the round is not added

#### Scenario: Too many active players
- **WHEN** more than 4 players are checked and "Add Round" is clicked
- **THEN** an error message is shown and the round is not added

### Requirement: Add Round resets card inputs
After successfully adding a round, all card-count inputs in the round-entry grid SHALL reset to 0.

#### Scenario: Inputs cleared after add
- **WHEN** the user clicks "Add Round" and the round is successfully added
- **THEN** all card-count inputs return to 0
