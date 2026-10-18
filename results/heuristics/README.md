# Heuristic results

This collection contains the revised-manuscript heuristic data: 5,147
conditions used in the analyses and eight supplementary MSLS conditions on
Instance 1. Every `.res` file has 100 trials with seeds 1--100, in that order.
`manifest.json` lists all 5,155 files, their SHA-256 checksums, parameters,
analysis roles, and final-cost descriptive statistics.

## Experiments and parameters

Instance 1 is used for parameter selection. The selected settings are then
fixed on Instances 2--5. Each run uses one thread; the time limit is user CPU
time, including initialization and local search.

| Target nodes (excluding the depot) | CPU seconds per trial, r = 50 | CPU seconds per trial, r = 100 |
| --- | ---: | ---: |
| 100 | 20 | 40 |
| 150 | 30 | 60 |
| 200 | 80 | 160 |
| 300 | 120 | 240 |

The fixed DR experiments test all four combinations of random destroy (RD),
cluster destroy (CD), random repair (RR), and greedy repair (GR), using
`alpha = 0.01, 0.02, ..., 0.14`. The same dense grid is used for the four
operator-selection policies: uniform independent (UI), uniform pair (UP),
adaptive independent (AI), and adaptive pair (AP). The adaptive experiments
use rewards 33, 9, and 13, a segment length of 100, and reaction factor 0.1.
The published CD data include the recomputed CD experiments.

For LOIO, the complete TS and fixed-DR grids are available on all five
instances at `n = 100, 150`. Large-instance TS grids are available on Instance
1; their selected settings are evaluated on Instances 2--5.

| Setting | TS t1 grid | TS t2 grid | Instances with full grid |
| --- | --- | --- | --- |
| n = 100, both radii | 8--22, step 1 | 1--6, step 1 | 1--5 |
| n = 150, both radii | 14--32, step 1 | 1--10, step 1 | 1--5 |
| n = 200, r = 50 | 18--38, step 2 | 1--12, step 1 | 1 |
| n = 200, r = 100 | 18--38, step 2 | 1--7, step 1 | 1 |
| n = 300, both radii | 24--44, step 2 | 1--7, step 1 | 1 |

`summaries/experiment_protocol.json` gives the selected parameters and
`summaries/README.md` identifies the summary files. Some source-directory
names identify separate execution batches. They do not indicate a different
evaluation protocol; use each manifest entry's parameters and analysis roles.

## File names and operator codes

For example,
`E100_1000.1_r50_lk_dr_dest1_rep0_alpha5_ite20.res` means Instance 1 with
100 nodes, covering distance 50, CD--RR, alpha = 5%, and a 20-second CPU limit.
The `1000` component identifies the 1000 by 1000 benchmark region.
For TS, `_t16_t4_` gives `(t1, t2) = (16, 4)`; `_ite20` again denotes the
CPU-time limit, not an iteration count.

For fixed DR, `dest0` is RD, `dest1` is CD, `rep0` is RR, and `rep1` is GR.
Matching destroy/repair codes 2, 3, 4, and 5 respectively denote UI, UP, AI,
and AP. AI selects destroy and repair operators separately; AP selects a
destroy--repair pair. For UI and UP, selection is uniform rather than
performance-dependent.

## Raw result columns

Files are whitespace-separated numeric text without a header. Column numbers
below are one-based. For a time limit of T seconds, there are `11 + 2*T` columns.

| Column | Meaning |
| ---: | --- |
| 1 | Trial seed, 1--100 |
| 2 | Cost after LK improvement of the full TSP tour |
| 3 | Percentage gap of column 2 to the TSP reference |
| 4 | Cost after the initial CSPNS local search |
| 5 | Percentage gap of column 4 to the CSPNS reference |
| 6 | Final best integer objective cost |
| 7 | Percentage gap of column 6 to the CSPNS reference |
| 8 | User CPU time in seconds |
| 9 | Iteration count |
| 10 | Candidate-evaluation count |
| 11 | Feasibility-check count |
| 12 onward | Best-so-far cost at 0.5, 1.0, 1.5, ..., T seconds |

Costs are integer travel-time objectives in seconds: each edge uses the
ceiling of its Euclidean travel time at 30 km/h. Some filenames and analysis
field names retain the historical term `length`; they refer to this cost.
A checkpoint value of `-1` means no incumbent was recorded at that time.

For MSLS, columns 2 and 4 can be overwritten at later restarts; they must not
be interpreted as the common initial LS result. The LS baseline in the paper
is obtained from column 4 of the selected TS file with the same seed. Likewise,
the LK initialization check uses column 2 of selected TS files, not MSLS files.

**The stored gap columns for n = 200 and 300 use dummy reference values and
are not meaningful.** Use column 6 and the checkpoint costs for those sizes.
For n = 100 and 150, calculate gaps from the integer cost and the relevant
file in `../../reference_values/`, rather than using rounded stored gaps.
A negative gap is possible if a heuristic improves an unproved Gurobi
incumbent.

## Summaries and statistical comparisons

Mean, best, worst, and sample standard deviation are calculated over each
condition's 100 integer objective values. The standard deviation uses
denominator 99. An average row averages the instance-level statistics; it
does not report extrema or standard deviation of pooled trials.

Paired tests use integer objective values matched by seed, not rounded gaps.
Zero differences are excluded and `n_eff` reports the remaining number of
pairs. The exact two-sided signed-rank calculation accounts for tied ranks.
If all differences are zero, `n_eff = 0` and p = 1. Holm adjustments use two
separate 32-test families for fixed DR versus TS/MSLS (small/medium and large),
and a separate 320-test family for all five DR policies. LOIO results use
training instances only for parameter selection; the held-out instance does
not influence that fold's choice.

The current-paper raw files were checked for 100 ordered seeds, the expected
column count, complete CPU budgets, integer final costs, and agreement of
the final checkpoint with the final cost. The eight supplementary MSLS
Instance-1 files passed the same checks. Partial per-seed files, failed runs,
obsolete short-budget grids, and unused reward-parameter diagnostics are
not included.
