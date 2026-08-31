# Model and Runtime Adaptation

Read this only when the user names a model, asks for migration, or the prompt's behavior clearly depends on current model capabilities. Models change fast; this file keeps the judgment discipline, not parameter tables that expire.

## Verify current facts first

Check the target model's latest official prompting, reasoning, tools, structured outputs, and migration docs. Keep the exact model the user specified — do not swap in a "newer" one on your own. Mark behavior the official material does not cover as pending validation.

If no target is specified, deliver a portable core first. Suggest candidates only when model differences would change results or cost, and put the selection rationale outside the prompt.

## Put each control back in its layer

- reasoning / thinking effort controls the internal computation budget;
- verbosity or output-token settings control default length;
- structured outputs / tool schemas control machine-parseable structure;
- temperature and sampling parameters follow the target model's current recommendations;
- permissions, tool allowlists, approvals, and business validation are enforced by the runtime;
- prompt caching needs a stable static prefix with dynamic input placed late.

The prompt describes only the task-specific goal, content priorities, evidence, constraints, and completion criteria. Do not control the same thing twice through runtime parameters and multiple natural-language commands.

## Migration discipline

First switch only the model, pin the original runtime baseline, and test on representative tasks. Then adjust one variable at a time: reasoning, prompt modules, tools, or schema. Rewriting the whole prompt at once makes it impossible to tell where a regression came from.

Delete the anti-laziness nudges, forced step-by-step thinking, repeated tool triggers, and verbose format scaffolding left over from older models — but only after evals prove the default capability already covers them. Put vendor-specific advice in adapter notes; do not pollute the portable core.

Done when: current-model facts come from official sources, the natural-language prompt and runtime configuration each do their own job, and migration can localize behavior changes through single-variable evals.
