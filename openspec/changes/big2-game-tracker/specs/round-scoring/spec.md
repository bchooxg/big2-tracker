## ADDED Requirements

### Requirement: Price per card configuration
The system SHALL provide a numeric input for "Price per Card ($)" with a minimum of 0.1, step of 0.1, and a default value of 1.

#### Scenario: Change price per card
- **WHEN** the user sets the price-per-card input to a new value before adding a round
- **THEN** that round is scored using the new price
- **AND** subsequent rounds retain the last set price as the default

### Requirement: Card count input per active player
The system SHALL display a number input (range 0–13) for each active player in the Round Entry section.

#### Scenario: Valid card count entry
- **WHEN** the user enters a number between 0 and 13 for each active player
- **THEN** the "Add Round" button accepts the input

#### Scenario: Invalid card count entry
- **WHEN** the user enters a value outside 0–13 for any active player
- **THEN** the system shows an error and does not add the round

### Requirement: Pairwise head-to-head scoring
The system SHALL compute scores by comparing every pair of active players. For each pair (A, B) where A has fewer cards than B, B pays A. The payment amount is determined by B's card count and the active price per card, with the following multipliers applied to B's card count:
- cards < 10 → 1× multiplier (payment = cards × price)
- 10 ≤ cards < 13 → 2× multiplier (payment = cards × price × 2)
- cards = 13 → 3× multiplier (payment = cards × price × 3)

After accumulating all pairwise payments, each player's net score for the round is divided by 2 to ensure the round sums to zero.

#### Scenario: Standard 4-player round
- **WHEN** four players with card counts 3, 7, 10, 13 and price $1 complete a round
- **THEN** pairwise payments are computed for all 6 pairs using the correct multipliers, divided by 2, and every player's net is stored

#### Scenario: Round sum is zero
- **WHEN** any round is added
- **THEN** the sum of all active players' scores for that round SHALL be zero (within floating-point tolerance of 0.001)

### Requirement: Balance check per round
The system SHALL compute the sum of all player scores for each round and display a balance status.

#### Scenario: Balanced round
- **WHEN** the sum of all player scores for a round is within 0.001 of zero
- **THEN** the Balance Check cell shows "✓ Balanced" in muted styling

#### Scenario: Unbalanced round (error state)
- **WHEN** the sum of all player scores for a round exceeds 0.001 in absolute value
- **THEN** the Balance Check cell shows "Error: $X.XX" in red

### Requirement: Reset card inputs after round added
The system SHALL reset all card count inputs to 0 after a round is successfully added.

#### Scenario: Inputs reset
- **WHEN** a round is successfully added
- **THEN** all card count fields in Round Entry show 0
