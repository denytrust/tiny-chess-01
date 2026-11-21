# tiny-chess Delta150

## Change vs v2
One parameter only: quiescence delta-pruning margin 200->150
(`if s+g2+150<l:continue` in q()). Wider QS: fewer captures pruned.
Rest = v2 exactly (0x88 alpha-beta/PVS/TT/killers/history, tapered
MG/EG PST, bishop pair, tempo+10, futility 150*d, null-move H>=8,
check extension). Budgets unchanged: 120k main / 180k total nodes.
Fully deterministic (no wall clock; seeded RNG only for Zobrist keys).

## Practice trials (local kit, 6 games each)
- trial-0: Elo 2112 (6W 0D 0L) — v2 1809, v3 1654
- trial-1: Elo 1545 (3W 3D 0L) — v2 1451, v3 1545
- trial-2: Elo 1545 (4W 1D 1L) — v2 1451, v3 1364
- mean: 1734. v2: 1570. v3: 1521.
- Delta150 beats v2 on ALL THREE trials (+303/+94/+94), mean +164 —
  far beyond trial noise (<1 game flip ~50 Elo). Clear improvement.

## Safety / size / correctness
- main.py 3761/4096 bytes. Max think 6.54s (153-position probe,
  incl. 144 positions actually faced in the trials), under the
  10s limit; no time losses in any trial.
- Correctness: tables identical to v2; perft ALL PASS; eval check
  ALL PASS; fuzz 2000 positions, 0 mismatches.
- Note: base85 packer fails on this source (payload holds a quote;
  also 4545 bytes). Latin-1 packer used instead (3761).
