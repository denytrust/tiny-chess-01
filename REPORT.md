# tiny-chess-01 — report

## Engine
0x88 board; alpha-beta + iterative deepening, PVS, null-move, quiescence
(delta pruning), Zobrist TT, MVV-LVA + killers + history, material + PST
eval. Fixed 200k-node budget/move (main + quiescence), no clock, no
randomness. `main.py` is the kit's makefun-compress/v1 packing (LZMA stub)
of the golfed source (`source.py`, 7,655 bytes, kept beside the entry);
stdlib only; talks to the harness over HTTP, no file or model access.

## Size
- main.py: 3,333 / 4,096 bytes
- repo total: 7,522 / 8,192 bytes

## Tests
- perft: startpos d3 8,902; Kiwipete d3 97,862 — pass.
- fuzz vs python-chess: 14,397 positions, 0 mismatches.
- practice trials (6 games), final main.py:
  - trial-0 (150k): 3W 1D 2L, Elo 1,364.
  - trial-1 (200k): 1W 4D 1L, Elo 1,279.
  - No time losses; max think 7.7 s (limit 10 s).
- dev engine (tapered, main-only 120k): trial-0 Elo 2,112, trial-1
  Elo 1,545 — stronger but does not fit 4 KB and times out.

## Verdict vs sunfish
Sunfish's 6-game practice mean is ~1,365 Elo. This entry's mean (~1,320)
is slightly below it, so it likely does NOT beat the house baseline.
Counting quiescence nodes (to stay under 10 s/move) cuts search depth.
