## ADDED Requirements

### Requirement: Save state to session storage
After every state mutation the app SHALL serialise the full game state (players and rounds) to `sessionStorage` under the key `'big2-state'`. The save MUST occur after every successful add, delete, edit, rename, add/remove player, and reset operation.

#### Scenario: State saved after adding a round
- **WHEN** the user clicks "Add Round" and the round is successfully added
- **THEN** `sessionStorage['big2-state']` is updated with the new round included

#### Scenario: State saved after adding a special combo
- **WHEN** the user confirms a Special Combo
- **THEN** `sessionStorage['big2-state']` is updated with the special combo round included

#### Scenario: State saved after renaming a player
- **WHEN** the user renames a player and the input loses focus
- **THEN** `sessionStorage['big2-state']` reflects the updated player name

### Requirement: Restore state on page load
On page load the app SHALL attempt to read and parse `sessionStorage['big2-state']`. If valid state is found it SHALL restore `players` and `rounds` and recalculate the internal ID counters before the first render. If the stored data is missing or invalid the app SHALL silently fall back to the default initial state (4 default players, no rounds).

#### Scenario: Refresh restores rounds
- **WHEN** the user has added one or more rounds and refreshes the page
- **THEN** the Game Results table shows the same rounds as before the refresh

#### Scenario: Refresh restores player names
- **WHEN** the user has renamed players and refreshes the page
- **THEN** the renamed player names appear in the roster and all column headers

#### Scenario: Corrupt storage falls back gracefully
- **WHEN** `sessionStorage['big2-state']` contains invalid JSON
- **THEN** the app loads with default state and no error is shown to the user

### Requirement: Reset Game clears session storage
When the user confirms Reset Game the app SHALL clear the persisted state from `sessionStorage` in addition to clearing rounds from memory.

#### Scenario: Reset clears storage
- **WHEN** the user clicks "Reset Game" and confirms
- **THEN** `sessionStorage['big2-state']` no longer contains round data (players may remain)
