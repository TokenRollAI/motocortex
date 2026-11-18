---
name: demo-sketch-first
description: >-
  Align on new features, moderately complex UI/UX interactions, and system
  architectures before coding by building playable visual Joplo demos and
  watching live reviewer feedback. Use before implementing greenfield features
  or non-trivial UI/UX interactions (multi-state flows, shortcuts/gestures,
  streaming/async states, cross-panel coordination), when comparing interaction
  options, when explaining technical architecture and end-to-end data pipelines
  with Joplo Diagrams, or when repairing unclear demo titles, abstract case
  names, slide-like cards, or missing `joplo feedback watch` loops. Do not use
  for trivial copy/CSS tweaks, static slide decks, or routine backend fixes
  whose UI and data contracts are already settled.
---

A demo or sketch exists to **show the user visually how a proposed design behaves, how data moves through the system, and what the finished implementation will feel like** — before committing production code. Always lead with a playable visual demo before coding a greenfield feature or any moderately complex UI/UX interaction; scale targeted demo repairs or architecture-only walkthroughs strictly to the part requested.

Run Joplo commands from the demo project directory so version-matched packages resolve. Read only the installed Joplo topics (`npx joplo skill`, `authoring`, `story`, `cases`, `review`, or enabled plugin guides) and sections of [references/visual-sketch-craft.md](references/visual-sketch-craft.md) relevant to your task, and share [templates/SKETCH-PLAN.md](templates/SKETCH-PLAN.md) first when framing or alternatives are still open.

## Structure around real choices and plain user situations

Match Joplo's structure to the decision on the table: build **one** viable design when the interaction direction is already settled (`feature()` with one `work()`, or standalone `work()` + `chapter()` when no feature review cases apply), and compare multiple `work()` options on identical starting state and inputs only when reviewers face a genuine choice. Keep `pick: null` on open choices and leave inferred rules marked `ai_assumption` / `pending`.

Make every sidebar label legible to a first-time reviewer without insider jargon ([references/visual-sketch-craft.md](references/visual-sketch-craft.md)):

- **Feature title and goal**: Name the concrete capability and visible payoff plainly; write `goal` around the actor, surface, and outcome (solution-neutral when comparing options, preserving user-chosen mechanics otherwise) rather than slogans or module IDs.
- **Options, cases, scenarios, and steps**: Name each option after the mechanism under evaluation; name each `case` after a recognizable starting situation paired with an observable screen `expected` outcome; give every `flow()` or `chapter()` a plain action-and-outcome title (never `Flow 1` or `happy`); and write concise step captions around the change the viewer needs to notice.

## Show expected UI behavior and trace data pipelines with Diagrams

Prove UI behavior visually on the surface where it lives — target context, active focus/cursor, input triggers, live progress, and before-vs-after state changes — rebuilding any static screen or bullet card as real interface state and motion.

Whenever backend boundaries, cross-service calls, or non-trivial data flows matter, explain the technical architecture in detail with `@joplo-app/plugin-diagram` (`Diagram`, `Sequence`, `StateMachine`) instead of prose summaries:

- **Anchor meaning, then trace every real hop**: Show the user-facing experience first when paired with UI, or start from the initiating caller in an architecture-only work. Group components by domain/ownership (`Diagram.Group` + `Diagram.Node`), and trace the data path from ingress through transformation and storage to consumer read-back — labeling payloads, state owners, `async` hops, and idempotency semantics on edges/messages.
- **Keep failure and guarantee claims honest**: Use `trace(...)` and `trace.fail(...)` to illustrate consequential failure or timeout recovery (including reconciling unknown write outcomes before retry), separating proposed design guarantees from source- or runtime-verified behavior rather than inventing nonexistent queues or rollbacks.

## Verify rendered frames, live playability, and active feedback reception

Inspect diagnostic counts from `npx joplo check` and `npx joplo outline` directly (since warnings still exit `0`), inspect rendered storyboard sheets (`npx joplo render --sheet` with `--out`), and play the decisive interaction once on the live board at the target viewport to confirm inputs, motion, contrast, and player overlay clearance — reporting explicitly if export browsers or localhost ports are blocked in the current environment.

Before sharing a board URL, wait for `npx joplo dev` to finish compilation, keep the owning board process alive, and verify `npx joplo feedback watch` is actively following the review rounds (matching local vs Cloud Share review surfaces and recovering closed rounds per session sequence when re-arming `--once`; see [references/visual-sketch-craft.md](references/visual-sketch-craft.md)). Acknowledge comments with their present location fields and approvals by `workId`/`revision`, inspect Alt-click targets with `npx joplo selection`, and write back `pick`, rule updates, or edits only within authorized scope (confirming `--public`/`--private` and `--review`/`--no-review` only when publication is requested).

## Done when

Scoped to the task: greenfield features and moderately complex UI/UX interactions are aligned through a playable visual demo before production coding; feature, option, case, and `flow()`/`chapter()` titles read as plain user situations; UI behavior is shown through real state transitions and any relevant technical architecture or data pipeline is traced clearly with `@joplo-app/plugin-diagram` without fabricated guarantees; `joplo check`/`outline` diagnostics, rendered sheets, and live board playback are verified (or environment limits reported honestly); and `joplo feedback watch` is actively receiving on the handed-off review surface with authorized conclusions applied cleanly.
