# Conflict-Driven Clause Learning (CDCL) in Ada 2023

Project Overview:
This repository provides a complete, strongly-typed implementation of the Conflict-Driven Clause Learning (CDCL) algorithm for solving the Boolean Satisfiability (SAT) problem. The CDCL algorithm systematically assigns truth values to variables, uses Boolean Constraint Propagation (BCP) to infer mandatory assignments, builds implication graphs, and analyzes conflicts using the First Unique Implication Point (1UIP) technique to learn new clauses. It features non-chronological backtracking (backjumping) which dramatically prunes the search space compared to classical DPLL.

Features:
* Solve_Basic: The core CDCL algorithm utilizing 1UIP conflict analysis and backjumping without modifying learned clause state.
* Solve_With_Restarts: Variant that periodically restarts the decision tree (resetting back to decision level 0) while keeping all learned clauses, avoiding heavy-tail behavioral bottlenecks.
* Solve_With_Clause_Deletion: Variant simulating practical memory limits by pruning old learned clauses when the formula outgrows a defined maximum capacity.
* Full strong typing: Variables, Literals, Clauses, and states leverage Ada's type safety rather than bare integers.

Usage:
A comprehensive standalone test suite doubles as the executable example (`tests.adb`). To run it:
$ make test
This will output test results across 15 automated suites. Ensure all assertions result in "PASS". 
A programmatic example includes defining a `Formula`, populating it via `Add_Clause`, and invoking `Solve_Basic (Formula, Assignment)`. The `Is_Satisfied` function validates output.

Testing:
The test suite incorporates Functional Correctness (valid SAT/UNSAT detection on small topologies), Edge Cases (empty formulas, trivial assignments), Error Handling (exceptions for literal index out of bounds or literal '0'), and Invariants (structural validity checking via `Is_Satisfied`). This verification and validation ensures robust usage even in boundary situations.

Building:
Prerequisites: GNAT Compiler supporting Ada 2022/2023 (`-gnat2022` enabled by default in Makefile).
Run `make all` to build the binary into the `bin/` directory, or `make clean` to remove artifacts. Code complies strictly with zero warnings under `-gnatwa`.
