## MODIFIED Requirements

### Requirement: Special Combo entry
The app SHALL provide an "Add Special Combo" button. When clicked it SHALL open a modal centred in the viewport regardless of scroll position. The modal SHALL be fully usable on viewports as narrow as 375px.

#### Scenario: Button triggers special combo flow
- **WHEN** the user clicks "Add Special Combo"
- **THEN** a modal opens for selecting the winner among currently active players

#### Scenario: Modal is centred on desktop
- **WHEN** the special combo modal opens on a viewport wider than 600px
- **THEN** the modal is visually centred both horizontally and vertically in the viewport

#### Scenario: Modal is centred on mobile
- **WHEN** the special combo modal opens on a viewport of 375px width
- **THEN** the modal is centred in the viewport, does not overflow the screen edges, and all controls are reachable

#### Scenario: Active player validation applies
- **WHEN** fewer than 2 or more than 4 players are active and the user clicks "Add Special Combo"
- **THEN** an error is shown and the modal does not open
