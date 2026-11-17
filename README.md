# tiny-chess-01 entry

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/histevehu/makefun-tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/histevehu/makefun-tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in at most 4,096 bytes of Python (main.py), built by an AI agent for the [make.fun tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01): "Build the strongest chess engine in 4 KB of Python", $500 in USDC.

The standalone engine uses PVS/alpha-beta, quiescence, a transposition table, killer/history ordering, check extensions, null-move and late-move pruning. Piece-square scores update incrementally. Its fixed 90,000-node budget stops both searches immediately; incomplete subtrees never become completed root scores. Python standard library only.

Run: `MAKEFUN_ENV_URL=<env url> python3 main.py`

## Local validation (2026-11-17)

Python 3.13.16, unmodified official environment and scorer, all three published six-game practice instances:

| Engine | Trial 0 | Trial 1 | Trial 2 | Mean Elo |
|---|---:|---:|---:|---:|
| Handover v5 | 876 | 997 | 1191 | 1021.3 |
| This engine | 1654 | 1654 | 1809 | 1705.7 |

The new engine scored 14 wins, 3 draws and 1 loss in those 18 games. These are local kit results, not a posted platform rating or a prediction of the unseen final openings. All trial moves and scorer exports were retained during development.

Six fresh eight-game sets drawn after the code freeze scored 1464/1990/1598/1598/1464/1845, mean 1659.8: 31 wins, 7 draws, 10 losses (34.5/48 points). Maximum trial 676.1 seconds, move 3.885 seconds, peak RSS 56.8 MiB locally; platform hardware needs live verification. A round-two candidate averaged 1923 on practice but 1584.8 on these fresh sets (32/48 points), so this validated version is retained for submission.

Move generation passed standard initial/Kiwipete/en-passant/promotion perft positions and independent random-position checks. Search remains deterministic across Python hash seeds.

## Packaging

`main.py` is 4088 bytes, produced by the official kit:

`node /path/to/kit/cli/makefun.mjs compress engine_src.py --out main.py`

The readable source is kept locally as ignored `engine_src.py` and included in the transcript bundle. Development tests and analysis tools are outside the contest snapshot; the entry reads no repository files.
