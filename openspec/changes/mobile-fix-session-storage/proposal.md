## Why

Two bugs degrade the user experience: (1) adding a round causes the page to zoom out on mobile because the results table is wider than the viewport and overrides the intended responsive layout; (2) refreshing the page wipes all game data, forcing users to re-enter every round from memory.

## What Changes

- Fix mobile viewport zoom: ensure the results table never forces a page-level zoom-out; restrict table width and enforce `overflow-x` scrolling at the container level rather than at the page level
- Add session storage persistence: save `state` (players + rounds) to `sessionStorage` after every mutation; restore on page load so a refresh does not lose data
- Add a visible "data will survive refresh" indicator and ensure Reset Game also clears session storage

## Capabilities

### New Capabilities

- `session-persistence`: Save and restore game state via `sessionStorage`; state survives page refresh within the same browser session but is cleared when the tab is closed or Reset Game is triggered

### Modified Capabilities

- `game-results-table`: Table container must never trigger page-level zoom on mobile; horizontal scrolling must be contained within the wrapper element
