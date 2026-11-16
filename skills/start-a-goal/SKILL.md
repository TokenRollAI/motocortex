---
name: start-a-goal
description: Carry a goal from clarification to verified completion with resumable execution state and runtime evidence.
disable-model-invocation: true
---

Own the user's goal through to verified completion. Execution documents exist to survive context resets and agent handoffs, not to create ceremony before real work begins: keep them terse, non-overlapping, and anchored to actual repository and runtime state.

## Reconcile intent against project reality

Inspect the request, relevant codebase state, and any existing goal package in parallel before trusting prior notes. Earlier documents prove only that prior work happened, not that it matches the current goal or current code. Resume a matching package after repairing stale facts; isolate unrelated goals in their own directory and record the active package path in `PROGRESS.md` so sibling links never resolve against the wrong goal. Fold new user instructions directly into the package without re-asking settled choices.

## Settle forks and wire a lean execution package

Clarify only where ambiguity could redirect scope, acceptance, or costly commitments. Pull in `grill` (or apply its discipline directly) with the facts already gathered, recording settled choices, reversible working assumptions, and blocking questions in `DECISIONS.md`. Skip interviews when intent and acceptance are already clear.

Keep each document in its own lane and cross-reference by ID instead of duplicating prose:

- **VISION** ([templates/VISION.md](templates/VISION.md)): desired outcome, non-goals, checkable success criteria, and representative user/failure cases — free of implementation prescription unless the user constrained it.
- **DOR** ([templates/DOR.md](templates/DOR.md)): verified stack conventions, runnable verification surfaces, external prerequisites, and concrete readiness gaps mapped to the exact work they block.
- **DOD** ([templates/DOD.md](templates/DOD.md)): traceable acceptance items and end-to-end checks, each paired with the command, live runtime procedure, or human review that proves it.
- **LOOP** ([templates/LOOP.md](templates/LOOP.md)): the active execution contract — autonomy boundaries, stage cadence, verification rigor, pivot rules when an approach stalls, and exact completion vs blockage conditions.
- **PROGRESS** ([templates/PROGRESS.md](templates/PROGRESS.md)): compact live ledger of current state, verified `DOD` evidence, active blockers, and the next highest-leverage move.

Scale document weight to task complexity: a focused goal needs tight bullets, while multi-milestone work earns milestone grouping only where real dependencies or acceptance gates exist.

## Pace execution from working demo to stage-end architectural review

Creating the package is setup, not a stopping point: share the package path and continue directly into authorized execution unless the user asked only for planning or handoff.

Do not run heavyweight architectural or full-spectrum reviews on every micro-turn — premature critique before behavior works stalls momentum and breeds speculative abstraction. Advance substantial work in a deliberate cadence: **prove the core shape with a working demo/vertical slice -> build out the implementation -> verify end-to-end functionality -> consolidate and merge major stage work -> run deep architectural review once real boundaries, coupling, and workload forces are visible in running code** (refactoring structure where proven seams demand it). Guard irreversible one-way risks (data loss, external contracts, security boundaries) upfront, keep per-turn checks fast and functional, and reserve deep structural review for major stage milestones and pre-completion convergence.

Batch or parallelize independent reads, checks, and orthogonal changes. Treat mismatches and failures as causal signals: fix root causes at the owning boundary rather than patching callers, mocking away broken integrations, or weakening `VISION` / `DOD` criteria to make red checks pass. Update stale docs when verified facts or current user instructions supersede them; bring genuine scope or acceptance trade-offs back to the user while continuing unblocked work.

Verify outcomes in the real runtime — test suites, builds, CLI runs, or live browser walkthroughs (`ego-lite` preferred when available) — and re-run checks whenever subsequent edits touch their blast radius. Persist evidence and state transitions incrementally in `PROGRESS.md` so an abrupt session end leaves the next agent ready to act without replaying chat history.

## Done when

The package is consistent with current user intent and repository reality, every `VISION` criterion and user case maps to `DOD` verification, major integrated work has passed stage-end architectural review without unaddressed structural debt, and every `LOOP` completion gate — including final-state regression and any required human acceptance — is backed by observed evidence. When external prerequisites or user-owned decisions block all remaining work, report a blocked handoff naming the exact missing input and gated items; blocked is unfinished, not complete.
