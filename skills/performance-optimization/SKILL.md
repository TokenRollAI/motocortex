---
name: performance-optimization
description: >-
  Design, diagnose, optimize, or review software performance from explicit
  workload goals and evidence. Use when latency, throughput, capacity, resource
  efficiency, large or unbounded data, blocking work, queueing, concurrency,
  batching, streaming, or a suspected performance regression materially affects
  the task. Do not use for routine development with no performance target,
  bottleneck signal, or credible scale risk.
---

Performance is a system's behavior **delivering useful results under a specific workload** — not how low-level the code looks, how much concurrency it uses, or how many hand-written optimizations it carries. Establish the user-visible outcome and the workload first, then change the part that limits them; optimization without a target and evidence only trades a simple system for a harder-to-maintain one.

## Define the performance contract first

Say who is waiting, what work is being processed, how load arrives, and what outcome counts as good enough. Pick the metrics the user actually cares about for this task: end-to-end latency and its distribution, throughput, concurrent capacity, startup or completion time, memory, network, cost, or resources per unit of work. Averages hide tails and bursts, and local metrics hide end-to-end waiting; do not substitute an easy-to-measure but irrelevant number for the goal.

For an existing system, reproduce the problem and establish a baseline on representative data, hardware, configuration, and load. For a new system with no measurable baseline, define the target and the workload model first; prototype, benchmark, or spike only the high-risk assumptions that decide the architecture's success — do not dress them up as production evidence. Obvious unbounded resource growth, serial waterfalls, or critical-path blocking may be handled at design time, but state the causality and the assumptions.

Performance work must not trade correctness for numbers. Fold result semantics, data freshness, consistency, failure handling, and resource ceilings into the same contract; a speedup obtained by skipping necessary work is a functional regression.

## Find what actually limits the system

Follow a representative request or data flow and observe where time and resources go, separating useful computation, I/O waiting, lock or scheduler contention, queueing, network and serialization, data movement, memory pressure, and downstream dependencies. Locate the limit with profiles, traces, query plans, load tests, runtime metrics, or a minimal reproducible benchmark; do not guess the bottleneck from the shape of the code.

Look at the end-to-end critical path and saturation points before local hotspots. A faster function does not mean a faster user, and more concurrency may only move the queue into the database or a downstream service. How latency, errors, and resource usage change under high load usually says more about capacity limits than single-shot speed on an idle system.

## Reshape the work to fit the load

Look first for ways to eliminate repeated work, reduce data volume and round trips, avoid coordination, or move non-essential work off the critical path. Changes to algorithms, data structures, data layout, and access patterns usually have more leverage than local syntactic tweaks; which transformation to apply is still decided by the limit you located.

Turning synchronous work asynchronous trades state and operational complexity for responsiveness and independent scheduling — appropriate when immediate completion is unnecessary and producer and consumer can decouple. Design result polling or notification, idempotency, retries, cancellation, timeouts, backlog ceilings, and failure ownership; if the caller needs the result immediately, an async wrapper does not remove the wait.

Batching raises throughput by paying a fixed overhead once, while increasing per-item waiting, working-set size, and failure blast radius. Bound batch size and maximum wait by the latency budget and resource ceilings — do not wait indefinitely for "a bigger batch".

Streaming fits unbounded input, progressive results, or data that cannot fit in memory whole. Feed consumer capacity back to producers, and design backpressure, bounded buffers and state, cancellation, ordering, and failure recovery; without these boundaries, a stream just renames a memory leak to a pipeline.

Add concurrency and parallelism only to work that is genuinely independent and has resources available. Bound concurrency, propagate cancellation and deadlines, and watch downstream capacity; past saturation, more workers add contention, queueing, and tail latency. Use caching only for work proven expensive and repeated, and treat keys, invalidation, freshness, stampedes, and permission semantics as correctness design, not a free speedup.

These are lenses for judgment, not a fixed order or default answers. When a simple synchronous flow meets the contract, keep it; do not introduce queues, streaming platforms, distributed caches, or extra services to look high-performance.

## Treat every change as an experiment

Validate one meaningful hypothesis at a time, comparing before and after under the same reproducible conditions as the baseline. Observe distributions and run-to-run variance — do not book noise as a win — and run functional plus under-stress correctness checks alongside. The gain must pay for the added code, state, dependencies, and operational burden; revert changes that fall inside the noise while adding complexity.

Turn the effective target into performance budgets, benchmarks, load tests, or production monitoring proportionate to the risk, so it cannot silently regress later. Expensive tests and load that could affect shared or production environments require confirmed scope and authorization first; prefer validating in an isolated, representative environment.

## Done when

The performance target, workload model, and correctness boundaries are explicit; an existing system has a reproducible baseline, or a new system's key assumptions have proportionate evidence; the bottleneck conclusion comes from end-to-end measurement, not guessing; the chosen transformations match the load shape and their costs; results beat the noise under comparable conditions while preserving correctness; the added complexity is worth the gain; and the key metrics have regression guards proportionate to the risk. Without validation in the target environment, mark the work as pending validation — do not claim the optimization holds.
