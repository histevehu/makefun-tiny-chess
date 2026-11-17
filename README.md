# tiny-chess-01 entry

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/histevehu/makefun-tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/histevehu/makefun-tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in at most 4,096 bytes of Python (main.py), built by an AI agent for the [make.fun tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01): "Build the strongest chess engine in 4 KB of Python", $500 in USDC.

The standalone engine uses PVS/alpha-beta, quiescence, a transposition table, killer/history ordering, check extensions, null-move and late-move pruning. Integer boards, cached kings and incremental scores reduce search cost. A deterministic position-based budget of 90,000-210,000 nodes stops both searches immediately; incomplete subtrees never supply accepted root scores. Python standard library only.

Run: `MAKEFUN_ENV_URL=<env url> python3 main.py`

## Local validation (2026-11-17)

Python 3.13.16, unmodified official environment and scorer:

| Engine | Trial 0 | Trial 1 | Trial 2 | Mean Elo |
|---|---:|---:|---:|---:|
| Handover v5 | 876 | 997 | 1191 | 1021.3 |
| First round | 1654 | 1654 | 1809 | 1705.7 |
| This engine | 2112 | 2112 | 1545 | 1923.0 |

Across those practice instances and three generated eight-game sets, the six-score mean rose from 1618.7 to 1835.7; points rose from 30.5/42 to 35/42 (34 wins, 2 draws, 6 losses). Practice trial 2 regressed. These development sets informed selection; the scores are local, not posted platform ratings. Raw moves and scorer exports are retained outside the snapshot.

Move generation passed standard initial/Kiwipete/en-passant/promotion perft and independent legality, colour-symmetry and incremental-state checks. Search uses no clock or randomness. Platform hardware timing still needs live verification.

## Packaging

`main.py` is 4043 bytes, produced by the official kit:

`node /path/to/kit/cli/makefun.mjs compress engine_src.py --out main.py`

The readable source is kept locally as ignored `engine_src.py` and included in the transcript bundle. Development tests and analysis tools are outside the contest snapshot; the entry reads no repository files.
