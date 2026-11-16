# Prompt Evaluation and Iteration

A prompt change is an empirical claim over an input distribution and target runtime. Without representative checks, a rewrite is a reasoned hypothesis, never a verified improvement.

## Build a discriminating eval set

Freeze baseline artifacts — original prompt, model snapshot, reasoning/sampling config, tool definitions, and test inputs — so diffs stay attributable. Pull cases from real production or session trajectories whenever available, covering five fault lines:

- **Core happy path** (non-regression on everyday work);
- **Hard boundaries** (ambiguous labels, dense multi-constraint inputs, edge scales);
- **Missing or unverified inputs** (tests whether the model asks, narrows, or hallucinates);
- **Noisy, reordered, or adversarial inputs** (conflicting context, distractor details, untrusted injection payloads);
- **High-cost domain failures** (unauthorized side effects, dropped negations/numbers, fabricated citations).

Keep a held-out slice when iterating repeatedly so tuning does not overfit the phrasing of three dev examples.

## Prefer deterministic checks over vibe grading

Grade with code first: exact answers, schema/AST/build checks, test suites, citation-to-source verification, and tool-call/permission traces. Use rubric-anchored LLM judges only for semantic or stylistic qualities deterministic code cannot check, calibrated against human spot-reviews. Never accept the evaluated model's ungrounded self-grade as proof.

## Measure tails alongside averages

Compare candidate against baseline on both pass rate and worst-case failure severity, tracking latency, token/reasoning cost, and tool-call churn where operational budgets matter. When a bundled rewrite regresses a case, bisect changed blocks or examples to isolate the culprit. If live execution is out of scope, deliver a compact test matrix with concrete inputs, pass criteria, and exact failure signals, labeling improvements as unverified until run.
