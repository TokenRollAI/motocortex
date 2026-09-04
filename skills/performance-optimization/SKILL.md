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

## Match the evidence to the task

Keep design, review, diagnosis, and implementation within the user's requested scope. A review may identify a credible risk and the measurement needed to resolve it without changing code or generating load. A diagnosis seeks a supported explanation; implementation must also demonstrate the change's effect. Use the sections below where they help answer that task, rather than treating them as a sequence every request must complete.

## Define the performance contract

Say who is waiting, what work is being processed, how load arrives, and what outcome counts as good enough. Pick the metrics the user actually cares about for this task: end-to-end latency and its distribution, throughput, concurrent capacity, startup or completion time, memory, network, cost, or resources per unit of work. Averages hide tails and bursts, and local metrics hide end-to-end waiting; do not substitute an easy-to-measure but irrelevant number for the goal.

For a measured diagnosis or optimization, establish a baseline on representative data, hardware, configuration, and load. For design or review without runtime access, state the workload assumptions and causal risks, and identify the smallest measurement that would confirm or refute them. Prototype or benchmark success-critical unknowns when the task authorizes it and the evidence would change the decision. Existing traces or benchmarks may already answer the question; do not recreate them merely to follow a process.

Performance work must not trade correctness for numbers. Fold result semantics, data freshness, consistency, failure handling, and resource ceilings into the same contract; a speedup obtained by skipping necessary work is a functional regression.

## Find what actually limits the system

Follow the request or data flow relevant to the suspected constraint. Profiles, traces, query plans, load tests, runtime metrics, or a minimal benchmark can distinguish computation, waiting, contention, data movement, and downstream limits. Choose evidence that can discriminate between plausible causes. Code structure can support a risk hypothesis, but a claim about the actual bottleneck needs representative measurement.

Look at the end-to-end critical path and saturation points before local hotspots. A faster function does not mean a faster user, and more concurrency may only move the queue into the database or a downstream service. How latency, errors, and resource usage change under high load usually says more about capacity limits than single-shot speed on an idle system.

## Reshape the work to fit the load

Look first for ways to eliminate repeated work, reduce data volume and round trips, avoid coordination, or move non-essential work off the critical path. Changes to algorithms, data structures, data layout, and access patterns usually have more leverage than local syntactic tweaks; which transformation to apply is still decided by the limit you located.

Turning synchronous work asynchronous trades state and operational complexity for responsiveness and independent scheduling — appropriate when immediate completion is unnecessary and producer and consumer can decouple. Design result polling or notification, idempotency, retries, cancellation, timeouts, backlog ceilings, and failure ownership; if the caller needs the result immediately, an async wrapper does not remove the wait.

Batching raises throughput by paying a fixed overhead once, while increasing per-item waiting, working-set size, and failure blast radius. Bound batch size and maximum wait by the latency budget and resource ceilings — do not wait indefinitely for "a bigger batch".

Streaming fits unbounded input, progressive results, or data that cannot fit in memory whole. Feed consumer capacity back to producers, and design backpressure, bounded buffers and state, cancellation, ordering, and failure recovery; without these boundaries, a stream just renames a memory leak to a pipeline.

Add concurrency and parallelism only to work that is genuinely independent and has resources available. Bound concurrency, propagate cancellation and deadlines, and watch downstream capacity; past saturation, more workers add contention, queueing, and tail latency. Use caching only for work proven expensive and repeated, and treat keys, invalidation, freshness, stampedes, and permission semantics as correctness design, not a free speedup.

These are lenses for judgment, not a fixed order or default answers. When a simple synchronous flow meets the contract, keep it; do not introduce queues, streaming platforms, distributed caches, or extra services to look high-performance.

## Treat every change as an experiment

Keep comparisons attributable: preserve comparable workload and environment conditions, and isolate changes when interacting hypotheses would make the result ambiguous. Observe distributions and run-to-run variance, with correctness checks appropriate to the failure risk. Noise is not a demonstrated gain. Keep added complexity only when its measured benefit or another agreed requirement justifies it; remove unsupported additions made during the optimization without disturbing unrelated work.

Turn the effective target into performance budgets, benchmarks, load tests, or production monitoring proportionate to the risk, so it cannot silently regress later. Expensive tests and load that could affect shared or production environments require confirmed scope and authorization first; prefer validating in an isolated, representative environment.

## Done when

For design or review, the relevant workload, target or target gap, correctness boundaries, and causal trade-offs are clear; findings distinguish evidence from assumptions and identify proportionate validation for unresolved risks. A useful review can be complete while a performance hypothesis remains unverified.

For diagnosis, the evidence supports the cause or narrows the remaining hypotheses to a concrete measurement gap; distinguish a confirmed diagnosis from an investigation blocked on that gap.

For implementation, comparable measurements show whether the agreed target is met beyond noise, correctness is preserved, added complexity earns its cost, and regression protection matches the risk. If the target is unmet or target-environment validation is unavailable, report that limitation rather than claiming a successful optimization.
