# CSPNS-DR benchmark instances and computational results

Benchmark instances and computational results for **A Destroy-and-Repair
Heuristic for the Covering Salesman Problem With Nodes and Segments**.

The heuristic data in this snapshot were updated on 17 October 2026 for the
revised manuscript. They include 5,155 complete parameter conditions, each
with 100 trials (515,500 trials in total). Of these, 5,147 conditions support
the manuscript analyses; eight MSLS conditions on Instance 1 are supplementary.
The Gurobi data were updated on 18 October 2026, including the certified
all-node TSP result for Instance 10 at `n = 150, r = 0` (optimal cost 1201).

## Contents

- `instances/`: 40 Euclidean benchmark instances, ten each for
  `n = 100, 150, 200, 300`. Each line is `node_id x_coordinate y_coordinate`.
- `reference_values/`: Gurobi objective values for
  `n = 100, 150`, with `r = 0, 50, 100`. Each file has ten values in instance
  order. A value may be an incumbent obtained within 12 hours rather than a
  proved optimum.
- `results/gurobi/`: 80 Gurobi logs: 60 for `n = 100, 150`,
  `r = 0, 50, 100`, and Instances 1--10; and 20 for `n = 200, 300`,
  `r = 50, 100`, and Instances 1--5. The directory also contains a manifest,
  numerical summaries, and the validated all-node TSP solution for
  `E150_1000.10_R0`.
- `results/heuristics/ts/`: tabu-search parameter grids and evaluations.
- `results/heuristics/dr/`: fixed-operator destroy-and-repair results.
- `results/heuristics/msls/`: multi-start local search with matched time budgets.
- `results/heuristics/dr_operator_selection/`: dense-alpha experiments and
  fixed, uniform, and adaptive operator-selection evaluations.
- `results/heuristics/manifest.json`: every published heuristic condition,
  its use, parameters, descriptive statistics, and SHA-256 checksum.
- `results/heuristics/summaries/`: parameter choices, held-out comparisons,
  convergence data, statistical tests, and leave-one-instance-out (LOIO)
  analysis in JSON format.

Heuristic comparisons use `r = 50, 100` and Instances 1--5. Parameters are
selected on Instance 1 and fixed for the comparisons on Instances 2--5.
The LOIO analysis uses all five instances for `n = 100, 150`. The common DR
grid is `alpha = 0.01, 0.02, ..., 0.14`. See
[the heuristic data guide](results/heuristics/README.md) for the raw column
format, time budgets, parameter grids, and provenance.

The raw files in this snapshot replace the earlier heuristic collection.
Obsolete short-budget runs, incomplete runs, and unused diagnostic experiments
are not included. Source code is not included.

## Citation

Please cite the associated paper when using these instances or results.
The dataset record is available at
[Zenodo, DOI: 10.5281/zenodo.22667863](https://doi.org/10.5281/zenodo.22667863).
The project page is
[CSPNS-DR benchmark results](https://takafumi-matsuura.github.io/CSPNS-DR-benchmark-results/).

## License

The repository is intended to be distributed under the Creative Commons Zero
v1.0 Universal license (CC0-1.0).
