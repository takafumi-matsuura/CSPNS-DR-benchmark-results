# CSPNS-DR benchmark instances and computational results

This directory contains the benchmark instances and raw computational results
used in the paper on the Destroy-and-Repair (DR) method for the Covering
Salesman Problem with Neighborhoods (CSPNS).

## Contents

- `instances/`: Euclidean benchmark instances for `n = 100, 150, 200, 300`.
  Each instance file contains one point per line in the form
  `point_id x_coordinate y_coordinate`.
- `reference_values/`: objective values obtained by Gurobi for the `n = 100`
  and `n = 150` instances. These are the reference values used to calculate
  the reported gaps. A value can be the best solution found within the
  12-hour limit when optimality was not proved.
- `results/gurobi/`: Gurobi log files for `n = 100, 150` and
  `r = 0, 50, 100`.
- `results/heuristics/dr/`: raw results of the Destroy-and-Repair method.
- `results/heuristics/ts/`: raw results of tabu search.
- `results/heuristics/msls/`: raw results of multi-start local search.

The heuristic result directories are organized by problem size and instance
number. Parameter settings and time limits are encoded in each file name.
For example, `dest`, `rep`, and `alpha` identify the DR operators and removal
parameter; `t1` and `t2` identify the two tabu-tenure parameters; and `ite`
identifies the run time limit in seconds. Each `.res` file contains the results
of the repeated trials for that condition.

The complete instance set is included. The paper uses ten instances for the
Gurobi experiments at `n = 100, 150`, and five instances per condition for the
heuristic comparisons. The raw heuristic directories also retain parameter
tuning and supplementary runs produced during the study.

## Citation

Please cite the associated paper when using these instances or results.

## License

The repository is intended to be distributed under the Creative Commons Zero
v1.0 Universal license (CC0-1.0).
