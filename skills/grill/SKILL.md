---
name: grill
description: >-
  Gather the project's context, then interview the user one question at a time
  about the decisions they may not realize are open, until every branch is
  settled and nothing is silently assumed. Writes the conclusions to
  DECISIONS.md. Use when a goal is still rough and needs pinning down before
  any work, or when another skill needs the context clarified.
---

Take the context in first, then question everything still unsettled until it is clean. This work stocks the shelves for DOR — the more thoroughly you ask now, the less an autonomous agent drifts later.

## Collect before you ask

Before asking anything, read in every piece of context you can reach: repository structure, existing docs, the technology stack (package.json / configs / CI), established conventions, recent hotspots in the git log. **Look up yourself any fact the environment can answer — never ask the user for it.** Sort the findings into two piles: **settled** and **open**. (If `start-a-goal` already collected this, use its conclusions — do not read everything twice.)

For a settled stack or existing convention, record it and confirm with the user in one sentence — do not re-interview. Spend the questioning budget only on decisions left hanging.

## Interrogate the open decisions

Work through the open pile one decision at a time. The aim is to surface questions **the user may not realize are open**: edge cases, failure paths, implicit premises, requirements that contradict each other.

Carry the questions with **AskUserQuestion**: one decision per question, the recommended answer as the first option marked "(Recommended)", the remaining options as genuine alternative branches. Before each question, give one sentence on why this decision is open and why it must be settled now, so the user chooses with context. Fall back to prose only for questions that cannot be enumerated into options.

Decisions belong to the user; factual gaps you fill yourself from the environment.

When the user is temporarily unreachable, do not deadlock: take the default that best fits the existing context, record the assumption explicitly, keep moving, and have the user ratify the batch later.

## Write it down — do not leave it in the conversation

Consensus that lives only in session context gets wiped by automatic compaction, and the framing step then has nothing to build on. Write the conclusions into `DECISIONS.md` — three sections suffice: **Settled** (existing stack / conventions), **Decided** (one line each: decision + one-sentence reason), **Assumptions on record** (defaults taken while the user was away, pending ratification). The framing step reads this file to write VISION and DOR; it never replays the conversation.

## Done when

The frontier is empty: every branch of the decision tree has been walked, nothing is silently assumed, and `DECISIONS.md` is on disk. Do not write further documents until the user confirms the consensus. Hand off to the framing step.
