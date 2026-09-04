# Prompt Evaluation and Iteration

Prompt optimization is only meaningful relative to a target model, a task distribution, and metrics. Without evals you may propose better-reasoned candidates, but you cannot claim an improvement.

## Establish a baseline

Preserve the original prompt, model snapshot, runtime parameters, tool set, and representative inputs so a comparison can distinguish the revision's effect from changes in its environment. Use observed baseline failures to guide changes when available; a requested rewrite can also begin from explicit hypotheses and be compared afterwards. For a new prompt, a minimal task statement can serve as the baseline.

Choose cases that can reveal the change's likely benefits and regressions, drawing from:

- the typical success path;
- real boundaries or hard cases;
- missing necessary information;
- conflicts, noise, or input-order variation;
- domain-specific safety or quality risks.

Prefer samples from real trajectories. When repeatedly tuning against a set, reserve held-out cases to detect overfitting; a small one-off revision may only need a representative comparison. Include unaffected behavior as well as the failures that motivated the change, because a local improvement can hide a broader regression.

## Choose metrics

Prefer executable or checkable metrics: correct answers, schema validators, tests, builds, citation correspondence, permission events, human preference. Then supplement with task completion, factual coverage, format, cost, latency, reasoning tokens, tool calls, and retries.

An LLM judge needs an explicit rubric, calibration samples, and human spot checks. Model self-assessment can generate candidate diagnoses; it cannot prove improvement on its own.

## Small-step ablation

Compare the requested revision against its baseline on the same samples. When the cause of a gain or regression is unclear, isolate modules, examples, reasoning configuration, or tool changes to learn what contributes. Single-variable experiments support attribution; they are a diagnostic technique, not a requirement to deliver a coherent rewrite as many separate edits.

Watch both average performance and worst-case failures. A prompt that scores higher on the dev set while adding overreach, hallucination, or cross-version volatility is not better. Re-run the regression after migrating models or tools; do not assume the old optimal format is portable.

## Deliver eval suggestions

When running evals in place is not possible, provide a small, concrete test table: input characteristics, expected behavior, failure signals, and the metrics to record. List unvalidated changes as hypotheses and point out the lowest-cost next experiment.

Done when: changes map to observed failures or explicit behavioral hypotheses, the comparison method is reproducible, and conclusions distinguish measured results from proposed tests. If execution is unavailable, the validation plan identifies concrete inputs, expected behavior, and remaining uncertainty without claiming an empirical improvement.
