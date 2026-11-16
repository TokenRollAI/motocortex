# AI and Agent Interaction

Probabilistic output and autonomous side effects make uncertainty, object-level editing, scoped approval, and cheap local recovery core structural requirements rather than polish.

## Frame capability in task terms and keep deterministic UI intact

Anchor empty prompts with concrete task-shaped examples and honest capability bounds so users never stare at a blank input guessing syntax. Keep structured controls (filters, checkboxes, direct manipulation, table sorts, delete buttons) for deterministic work; natural language earns its latency and ambiguity cost only on open-ended synthesis, fuzzy intent, cross-cutting transformation, and drafting.

## Land output in editable domain objects, not dead transcripts

Materialize generated output directly inside the target workspace object — inline document blocks, structured code diffs, editable table rows, or staged action cards (`before -> after -> apply`). Results trapped inside a chat scrollback cannot be selectively tweaked, diffed, or rolled back cleanly.

## Gate side effects by blast radius and delegation scope

Separate drafting from committing external state. Actions within an explicit user-configured rule and easy reversibility (auto-labeling or archiving messages) can execute visibly with one-click undo. Actions that send externally, spend money, publish, alter permissions, or delete irreversibly outside granted scope require an exact preview of affected targets/parameters and explicit human approval — re-prompting whenever targets, amounts, or scope drift from what was authorized. Expose live step progress, pending gates, pause/cancel, and manual takeover throughout multi-step agent runs.

## Calibrate provenance, granular repair, and partial failure

Distinguish verified system facts from model inferences, surfacing assumptions and clickable source provenance inline rather than dressing guesses in authoritative UI chrome. Make local repair cheaper than re-prompting from scratch: inline direct edits, scoped regeneration of a single section, one-click rejection, and version restore. On timeouts, refusals, or mid-run tool errors, preserve partial artifacts already produced, state what failed and why, and offer scoped retry or manual completion.

## Hold AI-generated UI code to full engineering discipline

When using a model to generate frontend code, constrain it explicitly to the product's existing information architecture, design tokens, shared components, and full control/view state machines (`pending`, `error`, `unknown`, `empty`, keyboard focus, non-color signifiers, inline error recovery). Verify generated interfaces by walking live flows rather than accepting a plausible screenshot.
