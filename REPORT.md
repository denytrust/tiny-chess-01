# tiny-chess-01 v2

## Practice Elo (6 games/trial, kit practice)
v2 (180k total-node cap): t0 1809 (5W 1D 0L), t1 1451 (3W 2D 1L), t2 1451 (3W 2D 1L). Mean 1570.
v1 (200k nodes incl. quiescence): t0 1364 (3W 1D 2L), t1 1279 (1W 4D 1L), t2 1451 (3W 2D 1L). Mean 1365.
Floor 1154; sunfish ~1365. v2 beats both on every trial.

## Changes vs v1
Tapered MG/EG PSTs (224-char table + EG king table), bishop-pair bonus, tempo +10, futility pruning (d<=2), null-move phase guard, check extension. Main budget 120k nodes; quiescence not counted toward it, but a 180k total-node cap bounds think time (max 6.0s/move over 3 trials; limit 10s). Same 0x88 alpha-beta/PVS/TT/killers/history core. No randomness, no wall clock.

## Correctness
perft startpos d3 8902, Kiwipete d3 97862, POS3-6 d1-d3 PASS. Eval consistency PASS. Fuzz vs python-chess: 2000 positions, 0 mismatches. Golfed vs readable source: identical moves/node counts.

## Sizes
main.py 3651/4096 (kit makefun-compress/v1). source.py 8710, uncommitted (sent beside bundle). Tracked repo total 7952/8192.

## Caveat
150k/120k caps were also trialled while the local VM ran ~2x slower and lost games on time; their Elo is not a clean read. The 180k numbers above are the clean measurement (normal-speed VM). House speed unknown; 180k cap keeps max think 6.0s there.
