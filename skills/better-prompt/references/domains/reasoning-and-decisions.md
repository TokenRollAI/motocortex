# Reasoning and Decisions

Applies to math, logic, diagnosis, planning, option comparison, and recommendation. The goal is to make the problem, constraints, and checks visible — not to dictate how long a chain of thought the model should produce.

## How to optimize

Write down the problem definition, knowns, unknowns, hard constraints, and the optimization objective first. Recommendation and comparison tasks also need the evaluation dimensions, who decides the weights, and which trade-offs must not be settled on the user's behalf.

Distinguish "needs the right answer" from "needs an auditable process". For the former, control the reasoning budget through the target model's reasoning/thinking configuration; for the latter, require checkable assumptions, formulas, evidence, key intermediate results, and verification — not a recital of the full hidden chain of thought.

When deterministic computation, constraint solvers, code execution, or search tools are available, require the model to use them and report the results. Do not let natural-language confidence stand in for a calculator, a solver, tests, or an independent source.

Fix the steps only when the procedure itself is a compliance process, a proof format, or a reproducible experiment. Otherwise let the model choose its own decomposition, and state which invariants the final answer must be checked against.

For decision outputs, separate facts, assumptions, inferences, and preferences. Require a recommendation with its conditions of applicability — do not enumerate every option just to look thorough.

## Minimal evals

- a direct problem, a combined-constraints problem, and one misleading distractor;
- whether the conclusion is stable when irrelevant wording or input order changes;
- whether every key constraint is satisfied;
- whether tool computations agree with the final answer;
- whether insufficient information surfaces the real gap instead of fabricated certainty.

Done when: the problem is computable or decidable, the constraints are checkable, the conclusion and its key grounds are auditable, and the reasoning budget is not controlled by prompt incantations.
