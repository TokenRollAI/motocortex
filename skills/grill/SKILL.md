---
name: grill
description: >-
  Clarify consequential open decisions from project context and a focused user
  interview, recording the results in DECISIONS.md. Use when a rough goal,
  conflicting requirements, or unresolved scope, acceptance, or costly choices
  prevent confident progress. Do not use for routine implementation choices
  that can be resolved from existing context.
---

Help the user settle the uncertainty that could change the outcome or cause expensive rework. Good clarification makes useful work possible and exposes important assumptions; it does not require predicting every future branch of the project.

## Investigate what matters to the decision

Inspect the context that can answer the current questions: relevant code, docs, configuration, established conventions, or prior decisions. Reuse findings supplied by the caller. Widen the search when a conflict or missing fact could change the recommendation; collecting unrelated context consumes attention without reducing decision risk.

Separate facts, user decisions, and working assumptions. Preserve settled choices unless new evidence or the user's request reopens them. Verify facts through available sources; when evidence is unavailable, expose the gap rather than treating a guess as a settled fact.

## Ask where the answer changes the work

Bring consequential choices to the user: intended behavior, scope, acceptance, conflicting priorities, or commitments costly to reverse. Explain why the choice matters now, recommend an option with its trade-off, and make the alternatives understandable. Handle ordinary reversible implementation details within the existing goal and authorization yourself.

Prefer one decision at a time when its answer shapes later questions. Group independent questions when that reduces interruption without hiding trade-offs. Use an available host question tool when suitable, or ask in prose when the tool is absent, unavailable in the current mode, or unsuitable for the question.

When the user is unavailable, continue work that does not depend on their decision. A low-cost, reversible assumption can support progress if it fits the existing intent and is recorded as an assumption. Silence cannot authorize scope changes, irreversible commitments, or acceptance changes; keep dependent work pending until the required answer arrives.

## Preserve decisions as they emerge

Record decisions and their reasons incrementally in `DECISIONS.md` using [templates/DECISIONS.md](templates/DECISIONS.md). Use the caller's goal directory or the repository's existing convention, and update the matching record without overwriting an unrelated goal. Persisting during clarification keeps resolved questions from being asked again after context loss.

Distinguish what is settled from what still needs a decision, and identify which work each open question blocks. Ask for confirmation when a consequential interpretation remains uncertain; an answer already given does not need a second approval ceremony.

## Done when

The next useful work has a clear goal and acceptance basis, consequential choices needed for that work are settled, and DECISIONS records the supporting facts, decisions, reversible assumptions, and deferred questions. If a necessary choice remains unanswered, hand off that specific blocker rather than claiming consensus. Stop asking when further answers would not change the work now authorized.
