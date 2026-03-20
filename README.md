# Big 2 Game Tracker

A lightweight, single-page web app for tracking [Big 2](https://en.wikipedia.org/wiki/Big_two) card game scores with automatic pairwise scoring and a running session summary.

**Live:** https://bchooxg.github.io/big2-tracker/

---

## Features

- **Pairwise scoring** — each player settles directly against every other player based on the card count difference
- **Multipliers** — 2× at 10–12 cards, 3× at 13 cards (full hand)
- **Special Combo rounds** — flat $3 per loser, winner collects from all
- **Configurable price per card** — set a custom $/card for any round
- **Edit & delete rounds** — fix mistakes after the fact
- **Dynamic players** — rename players; add or remove players before rounds begin
- **Game Results table** — horizontally scrollable on mobile, sticky Round column
- **Session Summary** — running totals showing net win/loss per player across all rounds
- **Session persistence** — state is saved to `sessionStorage` so a page refresh restores your game
- **Reset Game** — clears all rounds (keeps the player roster)

## Scoring Rules

For each pair of players in a round:

```
payment = (loser's cards − winner's cards) × price/card × multiplier(loser's cards)
```

The winner receives that amount from the loser. All transfers are zero-sum.

| Loser's cards | Multiplier |
|---|---|
| ≤ 9 | 1× |
| 10–12 | 2× |
| 13 | 3× |

**Special Combo** — the named winner collects $3 from every other player regardless of card counts.

## Usage

No installation required. Open `index.html` in any modern browser, or visit the live link above.

1. Optionally rename the four default players
2. Click **Add Round**, enter each player's card count and the price per card, then confirm
3. Use **Add Special Combo** for combo wins
4. Click any round row to edit or delete it
5. Click **Reset Game** to start a new session (player names are preserved)

## Tech

Single self-contained HTML file — vanilla JS, inline CSS, no build step, no external dependencies.
