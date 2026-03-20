## ADDED Requirements

### Requirement: Session summary cards
The system SHALL display summary cards below the Game Results table showing: Total Rounds, Biggest Winner, and Biggest Loser.

#### Scenario: Total rounds count
- **WHEN** rounds have been added
- **THEN** the "Total Rounds" summary card shows the count of all rounds (normal + special combo)

#### Scenario: Biggest winner display
- **WHEN** at least one round has been played
- **THEN** the "Biggest Winner" summary card shows the player with the highest cumulative score and their total (e.g., "Tin (+$12.00)")

#### Scenario: Biggest loser display
- **WHEN** at least one round has been played
- **THEN** the "Biggest Loser" summary card shows the player with the lowest cumulative score and their total (e.g., "Josh (−$8.00)")

#### Scenario: Summary updates after each change
- **WHEN** a round is added, edited, or deleted
- **THEN** all summary cards update immediately to reflect current totals

### Requirement: Reset Game
The system SHALL provide a "Reset Game" button that clears all rounds and resets all player totals to zero, while preserving the current player list.

#### Scenario: Reset clears rounds and totals
- **WHEN** the user clicks "Reset Game" and confirms
- **THEN** all rounds are removed, all player cumulative totals become $0.00, and the Game Results table is empty

#### Scenario: Reset preserves player list
- **WHEN** the user clicks "Reset Game"
- **THEN** the player names and player list are unchanged after the reset
