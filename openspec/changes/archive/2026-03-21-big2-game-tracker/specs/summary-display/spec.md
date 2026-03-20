## ADDED Requirements

### Requirement: Total Rounds card
The summary section SHALL display a "Total Rounds" card showing the count of all rounds (normal + special combo).

#### Scenario: Count increments on add
- **WHEN** any round (normal or special combo) is added
- **THEN** the Total Rounds count increases by 1

#### Scenario: Count decrements on delete
- **WHEN** any round is deleted
- **THEN** the Total Rounds count decreases by 1

### Requirement: Biggest Winner card
The summary section SHALL display a "Biggest Winner" card showing the player with the highest cumulative total and their amount formatted as "+$X.XX". If all totals are zero or no rounds exist, a neutral placeholder is shown.

#### Scenario: Biggest winner identified correctly
- **WHEN** one player has a higher cumulative total than all others
- **THEN** the Biggest Winner card shows that player's name and formatted positive amount

#### Scenario: No rounds shows placeholder
- **WHEN** no rounds have been played
- **THEN** the Biggest Winner card shows a neutral placeholder (e.g. "-")

### Requirement: Biggest Loser card
The summary section SHALL display a "Biggest Loser" card showing the player with the lowest (most negative) cumulative total and their amount formatted as "-$X.XX". If all totals are zero or no rounds exist, a neutral placeholder is shown.

#### Scenario: Biggest loser identified correctly
- **WHEN** one player has a lower cumulative total than all others
- **THEN** the Biggest Loser card shows that player's name and their negative formatted amount

#### Scenario: No rounds shows placeholder
- **WHEN** no rounds have been played
- **THEN** the Biggest Loser card shows a neutral placeholder

### Requirement: Reset Game button
A "Reset Game" button SHALL clear all rounds and reset all per-player cumulative totals to zero. Player names and roster SHALL remain unchanged.

#### Scenario: Reset clears rounds and totals
- **WHEN** the user clicks "Reset Game" and confirms the action
- **THEN** all round rows are removed, all cumulative totals become $0.00, and summary cards reset to neutral placeholders

#### Scenario: Reset preserves player roster
- **WHEN** the game is reset
- **THEN** all players (with their current names) remain in the roster and round-entry section
