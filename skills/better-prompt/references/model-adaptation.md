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

Use runtime settings for mechanical controls and the prompt for their task-specific meaning. For example, an output budget limits size while the prompt explains what must survive compression. Avoid duplicating the same control in several places when those versions could conflict.

## Migration discipline

Preserve a baseline that makes the migration's effects interpretable. When identifying the cause of a regression, hold other factors stable while changing the model, prompt, or runtime setting under investigation. If the user requests a combined redesign, evaluate it as a candidate against the baseline and use narrower experiments where attribution matters.

Replace legacy nudges, forced reasoning scripts, repeated tool triggers, and unnecessary format scaffolding with the goal or invariant they were meant to protect. Preserve requirements whose purpose still applies. Treat behavioral gains from simplification as hypotheses until tested, and put vendor-specific advice in adapter notes rather than the portable core.

Done when: current-model facts come from official sources, the prompt and runtime configuration have complementary roles, and the migration has a comparison method that can reveal regressions and investigate their causes.
