# Gurobi results

This collection contains 80 completed four-thread Gurobi 13.0.2 runs with a
configured time limit of 43,200 seconds:

- 60 runs: n = 100 and 150; r = 0, 50, and 100; Instances 1--10.
- 20 runs: n = 200 and 300; r = 50 and 100; Instances 1--5.

`manifest.json` records the condition, final incumbent, lower bound, reported
MIP gap, termination status, actual solver runtime, and SHA-256 checksum of
each log. Solver runtime is elapsed wall-clock time. A time limit may be
slightly exceeded during solver termination; the actual runtime and the
configured limit are recorded separately.

`summary.json` contains the six small/medium aggregate rows and all
instance-level results. The average runtime in the small/medium summary is
calculated using only instances for which optimality was proved; the maximum
runtime includes every instance. Objective values are feasible incumbents,
not lower bounds. Summary displays use two decimal places with half-up
rounding, while exact decimal means are retained in the JSON.

For n = 150, r = 0, Instance 10, the strict all-node TSP optimum is 1201.
The new log certifies a matching lower bound of 1201 and zero gap, after
38.51 seconds using four threads. The supplied
`solutions/E150_1000.10_R0.sol` and `validation/E150_1000.10_R0.json`
confirm one tour through all 151 nodes (150 target nodes plus the depot)
and the independently recomputed ceiling-rounded travel-time cost.
The updated ten-instance mean objective is 1200.40 and the mean solver
runtime is 66.045 seconds (displayed as 66.05 seconds).

The objective-only files in `../../reference_values/` are provided for
n = 100 and 150. For large instances, use the incumbent and lower bound in
the manifest; no proved optimum or dummy optimum is supplied. All 20 large
runs reached the time limit without proving optimality. The paper's held-out
large-instance comparison uses Instances 2--5; Instance 1 is also retained
here for completeness.

The heuristic raw results and their numerical analyses were not changed by
this Gurobi update.
