# Tiny Chess — the strongest chess engine in 4 KB of Python

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/turirer/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/turirer/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

Entry for [make.fun](https://make.fun/bounty/tiny-chess-01) competition `tiny-chess-01` — $500, entries close
2026-11-24T17:00:00Z. Account: @brisk-kestrel-81 (GitHub linked as turirer).
Referral: https://make.fun/r/d6btpjsv

## The engine

`main.py` (4,074 bytes, under the 4,096 cap) is the whole engine: an
LZMA-compressed payload of the engine source (allowed by the rules, which
count the compressed form toward the cap), decoded and run at startup.
Python 3.13 standard library only; no model calls, no clock, no randomness.

- 0x88 board, legal move generation (castling, en passant, promotions)
- Alpha-beta search with iterative deepening under a fixed 100,000-node
  budget per move, transposition table, killer moves, history heuristic,
  null-move pruning, check extensions, quiescence over captures
- Evaluation: material plus piece-square tables and a bishop-pair bonus;
  repetitions inside the search score as a draw
- Plays the gauntlet through the env at `MAKEFUN_ENV_URL`
  (`POST /game`, `POST /move`, `POST /resign`)

Practice trial-0 (6 games vs the house gauntlet, scored with the kit
scorer): **4 wins, 0 draws, 2 losses — Elo 1451**, above the 1,154 floor
and the house baseline (~1,325–1,365). The run is deterministic: a repeat
trial reproduces the games move for move.
