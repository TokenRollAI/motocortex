# AI and Agent Interaction

Model output is probabilistic and sometimes wrong, and agents can take actions with real consequences. The classic interaction principles still apply; what changes is that uncertainty, preview, approval, provenance, correction, and recovery become first-class parts of the interface rather than edge cases.

## Set expectations before the first interaction

Tell people what the system can do, how well it tends to do it, and where it is likely to fail, in terms of their tasks rather than model capabilities. Offer concrete starting points, such as examples or suggested requests, so users do not have to guess what to type.

## Keep structured UI for deterministic work

A chat box is not an information architecture. Search, selection, filtering, permissions, versions, approvals, and direct edits should stay available as structured controls; nobody should need to write a prompt to delete a row. Use natural language where it earns its cost: ambiguous intent, generation, transformation, and complex combinations that structured controls express poorly.

## Turn output into objects

Land generated results in the object they belong to, where people can inspect and edit them directly: a document in the editor, code as a diff, tasks in the task list, proposed changes as before, after, and apply. Output that only lives in a chat transcript cannot be manipulated incrementally or undone precisely.

## Separate drafting from acting

Generating a draft and performing a side effect are different risk levels. Place approval points by impact, reversibility, and the scope of authorization the user has already granted. An action inside an explicitly approved rule or delegation, such as archiving mail that matches a filter the user set up, can run without per-instance confirmation, provided it stays visible and reversible. An action that sends, publishes, pays, deletes irreversibly, changes permissions, or affects other people, money, or compliance outside that granted scope needs a preview of exactly what will happen and human approval. Ask again when the agent would exceed its granted scope or when a condition the authorization depended on has changed, such as recipients, amount, or target. Decide these approval points when designing the feature, not after an incident. Make agent progress, current step, and pending approvals visible, and let people pause, stop, or take over.

## Show uncertainty and provenance honestly

Do not present a model's guess as confirmed application state. Mark low confidence, state the assumptions the output relies on, and cite sources where claims depend on them. Ask a clarifying question only when an ambiguity would materially change the result; otherwise proceed with a stated assumption the user can correct.

## Make correction a first-class action

Beyond rating output, let people edit it, regenerate only one part, reject a suggestion, say "not what I meant" with a reason, and restore a previous version. Acknowledge feedback when it is received and, where applicable, explain how it will affect future behavior. A wrong result should be fixable locally without starting the whole interaction over.

## Handle failure gracefully

Design for refusals, timeouts, partial results, tool failures, and missing information. Keep whatever was produced, say what is missing and why, and offer a way forward: retry, narrow the request, fill the gap manually, or hand off to a person.

## Generating interfaces with AI

Using AI to generate UI does not mean the UI contains AI features; apply the sections above only when the product itself exposes AI behavior. Hold generated UI to the same scope discipline as hand-built work. Before generating, identify the flows the change actually touches, reuse the existing information architecture, tokens, components, and state definitions, and specify only what the change adds or alters. Adding an error message to an existing form needs that field's error, recovery, and accessibility behavior, not a new design system.

For the touched flows, make sure the generator is constrained on the lenses that apply: component states, feedback and recovery for asynchronous actions, the policy for destructive actions, keyboard and semantic markup, responsive behavior, and the view states the flow can reach. Hold the output to the same guardrails as hand-built UI: reuse conventions instead of inventing interactions, keep hover and color from being the only channel, keep errors out of toast-only channels, and give side-effecting actions a visible result before they apply.

Accept generated UI by the verification walk in the skill, not by how its screenshot looks.
