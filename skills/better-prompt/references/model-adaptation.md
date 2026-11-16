# Model and Runtime Adaptation

Load this when targeting a named model, migrating between model families or snapshots, or untangling prompt prose from API configuration. Vendor capabilities and parameters shift quickly; verify specifics against current official docs rather than relying on memorized folklore.

## Verify target-model behavior from primary docs

Look up the exact target model's official prompting, reasoning/thinking, tool-calling, and structured-output documentation. Keep the user's chosen model identifier intact rather than silently substituting another tier or vendor; offer model alternatives outside the prompt only when cost, latency, or capability trade-offs materially warrant it. Flag undocumented behaviors as hypotheses requiring empirical check.

## Assign each control to its native layer

Stop forcing prompt prose to do work the API or host runtime enforces deterministically:

- **Reasoning / thinking effort**: governs internal search and deliberation depth — tune via API config rather than prompt incantations.
- **Output / verbosity limits**: bound length via runtime budgets while using the prompt to specify *information priority* under compression.
- **Structured outputs and tool schemas**: enforce syntax, types, and enums in JSON Schema; reserve prompt space for semantic edge cases, nullability meaning, and precondition logic.
- **Authorization, sandboxing, and business invariants**: enforce in host code and server validators; prompts guide agent judgment, never replace access control.
- **Prompt caching**: keep static instructions, schemas, and reference context in a byte-stable prefix; append volatile session state, timestamps, and user turns last.

## Migrate with attributable baselines

Hold inputs, tools, and eval criteria constant when isolating whether a behavioral shift came from the model upgrade, runtime settings, or prompt edits. Strip compensations written for older, weaker models — repetitive tool-call reminders, rigid scratchpad templates, defensive formatting threats — and replace them only where the new model demonstrates an actual failure on the baseline set. Keep vendor-specific quirks in thin adapter notes outside the portable core.
