# Usability Evidence and Evaluation

Match evaluation cost to decision risk, and never conflate an evaluator's heuristic prediction with observed user behavior.

## Selecting discriminating evidence

Mine existing behavioral traces before commissioning new studies: funnel drop-offs and rage-clicks/undos show *where* friction concentrates (though traffic spikes can reflect misrouted navigation rather than demand), while support tickets and zero-result queries expose the exact vocabulary gap between user mental models and system labels.

Choose active methods by the unknown: **contextual inquiry** (watching real work in situ) before inventing a workflow; **iterative small-sample task walkthroughs** across each distinct persona to expose dominant comprehension and flow blockers rapidly; **card sorting / tree testing** to validate object hierarchy; and **controlled quantitative runs or production A/B telemetry** when sizing prevalence or comparing close contenders. State sample composition and blind spots explicitly whenever reporting findings.

## Severity calibration and comparative metrics

Heuristic inspection is fast, cheap, and noisy across single raters: synthesize independent passes where stakes are high, and rate every issue across three orthogonal axes — **frequency** (share of users exposed), **impact** (cost to overcome or recover), and **persistence** (whether knowing the quirk eliminates future hits or leaves a permanent tax) on a `0` (non-issue) to `4` (ship-blocker) scale, letting observed task failure override predicted severity.

Anchor quantitative comparisons against a baseline measured identically across the dimension at stake: **effectiveness** (completion, error, and clean recovery rates), **efficiency** (time on task, step/click count, backtracking), **post-task ease**, and **production friction signals** (abandonment, immediate undo rate, repeated retries, zero-result searches). Report every finding tied to persona, task, evidence class (`observed | measured | predicted`), causal mechanism, and convention-aligned fix.
