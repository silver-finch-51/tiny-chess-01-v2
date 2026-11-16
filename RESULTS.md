# Results — tiny-chess-01 v2 (round 2)

engine2.py (9,693 B) → main.py 4,034 B via kit `makefun compress`.
Ship spec: 45,000 nodes/move fixed, deterministic. Baseline ≈ 1,365.

## Runs (local, 2026-11-16)

| Run | Setting | G | W-D-L | Pts | Elo |
|---|---|---|---|---|---|
| Practice trial-0 @50k | gauntlet d2/d3/d4/100k/250k/500k | 6 | 4-1-1 | 4.5 | 1545 |
| Practice trial-1 @50k | same | 6 | 3-0-3 | 3.0 | 1279 |
| Practice trial-2 @50k | same | 6 | 3-0-3 | 3.0 | 1279 |
| Practice trial-1 @45k (ship) | same | 6 | 2-2-2 | 3.0 | 1279 |
| Head-to-head | v2@50k vs v1@40k, book | 12 | 8-0-4 | 8.0 | +120 vs v1 |
| Screening (dev build) | verbose v2 vs v1 @8k | 40 | 17-5-18 | 19.5 | −9 vs v1 |
| Smoke | custom vs depth-2 | 1 | 1-0-0 | 1.0 | — |
| Trial-0 attempt 1 | bot crashed (alias bug, fixed) | 0 | — | — | working 0 |

v1 on the same 3 practice trials: 10.5/18 pts, Elos 1191/2112/1099.
v2 @50k: also 10.5/18 pts, mean Elo 1,368.

Node budget: v1 shipped 40k after its 50k build forfeited a game on the 10 s
move cap (its git log). v2 @50k finished all 18 local trial games; 45k ships
for headroom and scored identically.

## What changed vs v1

- Incremental material/PST/phase state + piece sets: ~1.4× v1's nodes/sec.
- Futility pruning at depth ≤2; NMP gated on non-pawn material; one killer.
- Eval: bishop pair 30/45 + tapered passed pawns; PSTs decode as v1's.
- Cut to fit 4,096 B: king shield, isolated/doubled pawns, rook files,
  qsearch delta pruning (dev build only).

## Bottom line

Gauntlet: v2 level with the 1,365 baseline (mean trial Elo 1,368, same
points as v1). Head-to-head: +120 vs v1 (n=12). Clearing the prize gate is
plausible but not established — trial swings are ±250 Elo.
