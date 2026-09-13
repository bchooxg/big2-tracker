# Changelog

All notable changes to Big 2 Game Tracker are documented in this file.

## [1.2.0] - 2026-09-13
### Added
- Version number and in-app changelog viewer (footer link).

### Fixed
- Sticky table header: `.table-wrapper` now scrolls vertically within a capped height so player names stay visible while scrolling through rounds (previously the header only appeared to stick because of a CSS quirk that never actually kicked in on the page).

## [1.1.0] - 2026-09-13
### Added
- "Who Pays Who" settlement section: computes the minimal set of payments needed to settle all player balances using a greedy debt-simplification algorithm.
- Sticky table header (first attempt) so player names stay in view while scrolling.

## [1.0.0] - 2026-03-21
### Added
- Initial Big 2 Game Tracker: player management, round entry (normal + special combo), zero-sum pairwise scoring engine with card-count multipliers, results table with running totals and balance check, game summary stats.
- Mobile fixes: iOS Safari viewport/zoom fixes, numeric keypad inputs, responsive table layout, session persistence.
