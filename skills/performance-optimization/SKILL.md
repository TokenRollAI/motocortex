---
name: performance-optimization
description: >-
  Design, diagnose, optimize, or review software performance from explicit
  workload contracts and empirical evidence. Use when tail latency, throughput,
  concurrency, memory, I/O amplification, unbounded data, contention, queueing,
  batching, streaming, or a performance regression materially affects the work.
  Do not use for routine changes without a workload target, bottleneck signal,
  or credible scale risk.
---

Performance is **system behavior delivering correct results under a defined workload**, not clever micro-optimizations or gratuitous concurrency. Establish the workload contract and locate the dominant constraint empirically before mutating code; unmeasured optimization trades simplicity for superstition.

Match rigor to scope: a review identifies causal risks and the smallest measurement that settles them without inventing load; a diagnosis isolates the limiting factor with discriminating evidence; an implementation proves a material, reproducible win while preserving correctness.

## Lock the workload and correctness contract first

Specify who waits, workload arrival shape, data cardinality, concurrency, hardware/environment bounds, and the metric that actually matters — end-to-end tail latency (`p95`/`p99`), sustained throughput, peak memory/allocation rate, query/network amplification, cold-start time, or cost per unit work. Reject proxy averages and idle micro-benchmarks when user pain lives in tails, bursts, or end-to-end queueing.

Capture a reproducible baseline on representative data volume and concurrency before changing code (reusing existing traces, `EXPLAIN ANALYZE` plans, or benchmarks when valid). Fold correctness invariants — consistency, freshness, ordering, auth scoping, error semantics, and resource ceilings — into the contract up front; skipping required work is a bug, not a speedup.

## Isolate the real bottleneck on the critical path

Trace the end-to-end request or data path to separate CPU work, I/O round-trips, serialization cost, lock/pool contention, GC pressure, and downstream saturation. Use tools that discriminate between competing hypotheses — flamegraphs, execution plans, distributed traces, runtime counters, or a targeted reproducer — rather than guessing from static code shape.

Inspect saturation curves before local hotspots: shaving microseconds off a helper achieves nothing when a serial waterfall, N+1 query fan-out, or saturated connection pool dominates wall time, and raising worker counts past downstream capacity amplifies contention and tail latency.

## Apply the highest-leverage structural lever

Attack waste in descending order of leverage, guided by the measured constraint:

- **Eliminate and shrink**: delete redundant computation, collapse N+1 and chatty round-trips, push predicates/projections to storage, and trim payload/allocation volume before tuning syntax.
- **Decouple asynchronously** only when callers do not need synchronous results; design idempotency, bounded queues, timeouts, dead-letter/failure ownership, and status visibility — wrapping a blocking wait in `async` changes nothing if the caller still awaits it.
- **Batch** to amortize fixed per-call overhead when latency budgets permit, bounding both max batch size and max flush delay while isolating per-item failures.
- **Stream** unbounded or large payloads with explicit backpressure, bounded buffers, cancellation propagation, and mid-stream failure semantics; an unbounded stream is just a deferred OOM.
- **Parallelize** genuinely independent work within bounded worker/connection pools and propagated deadlines.
- **Cache** only work proven expensive and repeated, treating key scoping (especially tenant/auth boundaries), invalidation, staleness windows, and stampede protection as first-class correctness requirements.

Keep synchronous, uncached code whenever it meets the contract.

## Run attributable experiments and delete non-winners

Hold workload, data, and environment constant across before/after runs, isolating interacting edits when attribution would blur. Measure distributions across repeated runs so variance is never mistaken for improvement, and verify functional invariants alongside speed.

Revert any added complexity whose measured gain stays within noise or fails to justify its maintenance and operational tax. When a change ships, lock the gain behind proportional regression guards — query/allocation assertions, benchmark budgets, or production SLO telemetry. Obtain explicit authorization before running heavy load against shared or production infrastructure.

## Done when

For review or design, workload assumptions, causal bottleneck risks, correctness bounds, and the minimal discriminating measurement are explicit. For diagnosis, runtime evidence isolates the limiting mechanism or pinpoints the exact observability gap blocking confirmation. For optimization, repeatable before/after measurements on representative load demonstrate a material gain beyond variance, all correctness invariants hold, non-winning complexity is removed, and proportional regression protection or remaining environment gaps are stated honestly.
