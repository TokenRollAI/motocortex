---
name: start-a-goal
description: >-
  Take a goal from clarification to verified completion, with durable decisions,
  execution documents, and evidence that another agent can resume.
disable-model-invocation: true
---

Carry the user's goal through to a verified result. Use documents to preserve intent, decisions, and evidence across context loss and handoffs; let the work's dependencies and feedback determine how to get there. The documents support execution rather than prescribe a universal sequence.

## Establish which goal the documents describe

Recover the current goal and authorization from the user's request and relevant project context. Existing files are evidence of earlier work, not proof that the user wants that work resumed. Compare any existing VISION, DOR, DOD, LOOP, and PROGRESS with the current goal, their recorded state, and the actual project before relying on them.

Resume a matching, usable package. Repair missing or stale documents from supported decisions and current evidence before executing work that depends on them; file existence alone does not establish readiness. Incorporate changes the user has already requested without asking for the same decision again. When the intended goal or a material conflict cannot be resolved from context, ask the narrow question that resolves it and continue independent work.

Keep unrelated goals separate. Use the repository's established location, or a goal-specific directory when another package already occupies it. Preserve existing work and record the active package path in PROGRESS; resolve package links from that location so a handoff cannot accidentally load a different goal.

## Make the goal executable

Clarification is valuable where uncertainty could change the outcome or cause expensive rework. Use `grill` for those open decisions, passing along context already gathered. If it is unavailable, apply that same judgment directly: inspect discoverable facts, surface consequential choices, and record decisions and their reasons in DECISIONS. A clear request does not need an interview merely to fill a document.

Use DECISIONS as the durable record of settled choices, assumptions, and unresolved questions. New user instructions supersede older records; reconcile the documents with those instructions rather than treating an old file as stronger authority. Unresolved choices constrain the work that depends on them, not every useful action.

Give the execution documents distinct jobs:

- **VISION** describes the desired outcome, scope, success criteria, and representative user cases. Keep implementation detail here only when it is a genuine user constraint.
- **DOR** identifies readiness gaps and the work each gap blocks, including settled technical choices and their basis.
- **DOD** makes every success criterion and user case traceable to acceptance evidence. Choose commands, repeatable user procedures, or explicit human review according to what can actually prove the result.
- **LOOP** records how to preserve intent, evaluate progress, and recognize completion or blockage within the task's authorization.
- **PROGRESS** carries the current state, evidence references, blockers, and useful next work. Keep it consistent with DOD and inherit DOR's unresolved dependencies.

Use the artifact skeletons in [VISION](templates/VISION.md), [DOR](templates/DOR.md), [DOD](templates/DOD.md), [LOOP](templates/LOOP.md), and [PROGRESS](templates/PROGRESS.md), adapting their sections to the goal. Organize work into milestones where they help explain dependencies or acceptance; a phase number is not itself a dependency.

## Execute with evidence and judgment

Use the package's LOOP contract to guide continued work. Choose useful work that is authorized and unblocked; combine related changes or revisit earlier work when feedback warrants it. Record decisions and meaningful results as they become available, especially before a handoff, so recovery does not depend on remembering an uninterrupted conversation.

Treat an implementation mismatch as a reason to investigate. Correct the implementation when it violates the agreed goal. Correct stale documentation when the user's existing instructions or established facts support the correction. Changes to user-owned scope, outcomes, or acceptance require the user's decision; difficulty implementing a requirement is not evidence that it should disappear.

Show the user the package paths once ready and continue the authorized work unless they requested a handoff. The generated documents do not grant additional permissions or override host instructions. If execution is interrupted, leave enough state for the next session to resume from the same goal and verify which evidence still applies.

## Done when

The package is ready when it describes the current goal consistently, acceptance covers every success criterion and user case, and unresolved decisions and prerequisites are linked to the work they affect. The goal is complete when the LOOP completion conditions are satisfied by evidence for the final state, including required regression and human acceptance. When only external inputs or user decisions can unlock remaining work, report a blocked handoff with the exact missing input and affected work; blocked is not complete.
