# Prompt Evaluation and Iteration

Prompt optimization is only meaningful relative to a target model, a task distribution, and metrics. Without evals you may propose better-reasoned candidates, but you cannot claim an improvement.

## Establish a baseline

Keep the original prompt, model snapshot, runtime parameters, tool set, and representative inputs. Run the baseline first, record the failure types, then decide what to change. When generating from scratch, use a minimal prompt as the baseline.

The eval set covers at least:

- the typical success path;
- real boundaries or hard cases;
- missing necessary information;
- conflicts, noise, or input-order variation;
- domain-specific safety or quality risks.

Pick samples from real trajectories and keep a held-out set that never touches the optimization. Do not score only against the failure cases that motivated the current change.

## Choose metrics

Prefer executable or checkable metrics: correct answers, schema validators, tests, builds, citation correspondence, permission events, human preference. Then supplement with task completion, factual coverage, format, cost, latency, reasoning tokens, tool calls, and retries.

An LLM judge needs an explicit rubric, calibration samples, and human spot checks. Model self-assessment can generate candidate diagnoses; it cannot prove improvement on its own.

## Small-step ablation

Add, remove, or rewrite one meaningful module at a time and re-run the same samples. Compare the bare/core prompt, domain modules, few-shot examples, reasoning configuration, and tool changes to find what actually contributes quality.

Watch both average performance and worst-case failures. A prompt that scores higher on the dev set while adding overreach, hallucination, or cross-version volatility is not better. Re-run the regression after migrating models or tools; do not assume the old optimal format is portable.

## Deliver eval suggestions

When running evals in place is not possible, provide a small, concrete test table: input characteristics, expected behavior, failure signals, and the metrics to record. List unvalidated changes as hypotheses and point out the lowest-cost next experiment.

Done when: every change maps to an observed failure mode, there is a reproducible baseline and comparison method, and the conclusion separates measured results from pending hypotheses.
