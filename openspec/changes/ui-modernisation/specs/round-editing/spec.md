## MODIFIED Requirements

### Requirement: Edit modal opens with current values
Clicking the edit button on a normal round SHALL open a modal centred in the viewport regardless of scroll position. The modal SHALL be fully usable on viewports as narrow as 375px.

#### Scenario: Modal pre-populated
- **WHEN** the user clicks edit on a round
- **THEN** a modal opens showing each player's current card count and active/inactive status for that round

#### Scenario: Modal is centred on desktop
- **WHEN** the edit modal opens on a viewport wider than 600px
- **THEN** the modal is visually centred both horizontally and vertically in the viewport

#### Scenario: Modal is centred on mobile
- **WHEN** the edit modal opens on a viewport of 375px width
- **THEN** the modal is centred in the viewport, does not overflow the screen edges, and all controls are reachable
