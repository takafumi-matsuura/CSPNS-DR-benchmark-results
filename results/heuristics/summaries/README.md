# Summary data

All JSON paths are relative to the repository root. All source `.res` files
are listed with SHA-256 checksums in `../manifest.json`. Raw costs, rather
than rounded percentage-gap columns, are the basis of the summaries.

- `experiment_protocol.json`: time budgets, grids, selected parameters, and
  the mapping between public method labels and raw operator codes.
- `instance1_dr_sensitivity.json`: all 448 fixed-pair and 448 operator-selection
  conditions on Instance 1, with the dense 1%--14% alpha grid.
- `heldout_comparison.json`: Instances 2--5 for fixed DR, TS, MSLS, UI, UP, AI,
  and AP; per-trial final costs, instance-mean checkpoint curves, group
  convergence curves, 64
  baseline tests, and 320 five-policy tests. `lengths` and `curves` are costs
  in seconds, despite the historical field names.
- `small_medium_statistics.json`: the four descriptive statistics, including
  the LS baseline extracted from the selected TS files, for n = 100 and 150.
- `loio_analysis.json`: all 40 folds, parameter-selection frequencies,
  held-out gaps and regret, plus all 3,920 input conditions for the dense-grid
  LOIO analysis at n = 100 and 150.

`Fixed` in these files is the fixed-pair DR baseline; `Uniform-independent`,
`Uniform-pair`, `Adaptive-independent-13`, and `Adaptive-pair-13` respectively
correspond to UI, UP, AI, and AP. The suffix `13` identifies the adaptive
reward for accepted, previously unseen worse solutions. Equal-cost or
previously seen solutions receive zero reward.

These files summarize the heuristic experiments. Gurobi logs and numerical
summaries are supplied separately in `../../gurobi/`, updated on 18 October
2026. The revised TSP reference for Instance 10 does not affect these
heuristic summaries, which use Instances 1--5.
