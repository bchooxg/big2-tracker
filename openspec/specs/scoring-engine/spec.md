### Requirement: Pairwise head-to-head scoring
For each round, the scoring engine SHALL compute a score for every ordered pair of active players. The player with the lower card count wins; the player with the higher card count loses.

#### Scenario: Two-player round basic payout
- **WHEN** Player A has 3 cards and Player B has 7 cards and price is $1
- **THEN** Player A receives +$7 raw and Player B receives -$7 raw (before halving)

#### Scenario: Equal card count yields zero transfer
- **WHEN** two active players have the same card count
- **THEN** neither player gains or loses from that pair

### Requirement: Card-count multiplier
The payout for a losing player SHALL be multiplied based on their remaining card count:
- 1–9 cards → 1× (no multiplier)
- 10–12 cards → 2× per card
- 13 cards → 3× per card

#### Scenario: Multiplier 2× applied at 10 cards
- **WHEN** the loser has 10 cards and price is $1
- **THEN** the raw transfer for that pair is $10 × 2 = $20

#### Scenario: Multiplier 3× applied at 13 cards
- **WHEN** the loser has 13 cards and price is $1
- **THEN** the raw transfer for that pair is $13 × 3 = $39

#### Scenario: No multiplier below 10 cards
- **WHEN** the loser has 9 cards and price is $1
- **THEN** the raw transfer for that pair is $9 × 1 = $9

### Requirement: Halving for zero-sum balance
After accumulating all pairwise raw transfers into each player's running total for the round, the engine SHALL divide every player's total by 2 to produce the final per-player score for that round.

#### Scenario: Three-player round sums to zero
- **WHEN** three players complete a round and their final scores are computed
- **THEN** the sum of all three final scores is 0 (within floating-point tolerance of $0.01)

#### Scenario: Four-player round sums to zero
- **WHEN** four players complete a round
- **THEN** the sum of all four final scores is 0 (within $0.01 tolerance)

### Requirement: Floating-point rounding
All monetary values SHALL be rounded to 2 decimal places (cents) after each computation step.

#### Scenario: Result rounded to 2 decimal places
- **WHEN** any intermediate calculation produces more than 2 decimal places
- **THEN** the displayed and stored value is rounded to exactly 2 decimal places
