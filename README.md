# Keyboard Combine

A gamified touch-typing trainer built for two kids (11 and 12) who would rather be
at swim practice. It teaches correct finger placement from the home row outward and
drills the opposite-hand Shift rule, then hides that practice inside a racing game,
boss fights and a sports/Marvel trivia sprint.

**Play it:** open `index.html` — that's the whole app. No build step, no dependencies,
no server. One file.

## What's in it

| Mode | What it trains |
| --- | --- |
| **Training Camp** | 12 drills: home row → top reach → bottom row → capitals → sentences. 95% accuracy to advance. |
| **The Forty** | Head-to-head race against a bot or another player's ghost. Three skins: gridiron, pool, night run. |
| **Boss Fight** | Four bosses. Finish a word to land a hit; let the fuse burn and it hits back. Captain Capslock is a pure Shift drill. |
| **Trivia Sprint** | Guess the answer, then type it exactly. Teams, swimming, jiu-jitsu, Marvel, Big Bang Theory. |
| **Coach's Board** | Standings, WPM trend, practice volume, per-key miss rates, and Shift-hand accuracy. |

## Teaching model

- Every key is colour-coded to the finger that owns it, shown on a live keyboard and
  a pair of animated hands.
- **Wrong keys block.** You cannot move past a character until it is correct, so bad
  habits never get rewarded with progress.
- **Shift is checked by hand, not just by result.** The app reads `event.code` to see
  whether `ShiftLeft` or `ShiftRight` was held. A capital on a left-hand letter
  requires the right Shift and vice versa; using the wrong one still types the letter
  but is logged and corrected on screen. Caps Lock is flagged too.
- Per-key hit/miss counts feed the Coach's Board, so you can see *which* keys are
  costing accuracy rather than just the overall number.

## Data

Stats are stored per player in `localStorage` under `kc.players.v1`, keyed by a slug
of the player's name. Nothing leaves the browser. Clearing site data resets progress.

When the same page runs as a Claude Artifact it additionally syncs those records to
the artifact's shared database, which is what makes one leaderboard work across
several devices. That code is feature-detected and no-ops everywhere else, so this
copy runs fine standalone.

## Customising

Everything a kid cares about lives in a few arrays near the top of the script:

- `LESSONS` — the drill ladder (`nk` is the new keys, `lines` are what gets typed)
- `BANKS` — themed word pools used by the race and the bosses
- `TRIVIA` — questions, with `alt` for accepted alternate answers
- `BOSSES` — names, HP, damage, fuse length and word pool
- `KITS` — the team colourways used for helmets and sprites

## Licence

MIT.
