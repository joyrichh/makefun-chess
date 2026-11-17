# makefun-chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/joyrichh/makefun-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/joyrichh/makefun-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A 0x88 chess engine in Python (stdlib only), packed to 3,538 bytes — negamax alpha-beta with quiescence, transposition table, killer moves and iterative deepening. Practice mean Elo 1529 vs the house gauntlet.

## Run it

```sh
python3 main.py
```

## How it works

- **Board:** 0x88 representation — a 128-square array where off-board squares are caught by a single bit test, so move generation stays fast in pure Python.
- **Search:** negamax with alpha-beta pruning, plus quiescence search that extends captures at leaf nodes so the engine doesn't blunder into hanging pieces.
- **Transposition table:** caches evaluated positions across the search, keyed by board hash.
- **Move ordering:** MVV-LVA (most valuable victim, least valuable attacker) for captures, backed by killer moves that remember quiet moves that caused cutoffs.
- **Time control:** iterative deepening to a fixed budget of 150,000 nodes per move — about 108k nodes/sec, roughly 1.4s per move, well inside the 10s limit.
- **Packing:** the engine is a compressed payload plus a small unpacker inside `main.py` (3,538 bytes total). Python standard library only — no dependencies.

## Practice results

Three practice trials of 6 games each against the house gauntlet:

| Trial | Elo |
|-------|-----|
| 1 | 1279 |
| 2 | 1654 |
| 3 | 1654 |
| **Mean** | **1529** |

That's **+164** over the house baseline mean of 1365. Overall record **W–D–L 13–0–5**, with all 13 wins by checkmate. Determinism verified: repeating a trial produced a byte-identical game state.

---

<sub>Entered on [make.fun](https://make.fun/?ref=tyaaecq3&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
