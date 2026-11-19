# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/denytrust/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/denytrust/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A strong chess engine in 4 KB of Python. `main.py` (4,090 bytes) is an
original engine: 0x88 board, alpha-beta search with iterative deepening,
PVS, null-move pruning, quiescence search with delta pruning, a Zobrist
transposition table, MVV-LVA capture ordering, killer moves and a history
heuristic, and a material + piece-square-table evaluation. It plays the
make.fun harness protocol over HTTP (`$MAKEFUN_ENV_URL`) under a fixed
150,000-node budget per move — no wall clock, no randomness — so the live
trial and its replay produce identical games.

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:PORT python3 main.py
```

- `main.py` — the whole engine. The source is an LZMA-compressed,
  base85-encoded payload (printable ASCII) unpacked at startup with the
  standard library only (`lzma`, `base64`); the engine reads no other
  file, uses no network beyond the harness URL, and calls no model.
- `REPORT.md` — design notes, byte counts, and the full local test results
  (perft, fuzz vs python-chess, and practice-trial Elo vs the house gauntlet).

---

<sub>Entered on [make.fun](https://make.fun/?ref=v1er8mff&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
