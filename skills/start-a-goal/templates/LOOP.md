# LOOP template

Adapt this contract to the goal's dependencies, verification needs, and existing authorization. Fill the package path relative to the repository root; use that path in the launch text. Paths to sibling documents resolve from this file's directory.

<loop-template>
# LOOP (execution contract)

## How to launch

Read `<goal-directory>/LOOP.md` and its sibling PROGRESS.md. Confirm that their goal matches the current request, then continue authorized work using VISION.md for intent and DOD.md for acceptance. Preserve useful state for the next session if execution is interrupted.

## Preserve the goal

User intent and authorization govern this package. Keep VISION, DOD, and the decision record consistent with the user's current instructions. Repair an implementation that violates the agreed outcome; revise a stale document when existing instructions or verified facts justify it. Obtain the user's decision before changing user-owned scope, outcomes, or acceptance unless that change is already authorized. Record the reason so the next agent can distinguish a correction from a new requirement.

## Choose useful work

Let actual dependencies, risk, and feedback determine the next work. Milestones organize the goal; they do not prohibit advancing independent work elsewhere. Related items may be handled together when that makes implementation or verification clearer.

Use the tools, delegation, and commits supported by the host and authorized for this task. This document supplies no additional permission. Choose execution mechanics for the work at hand rather than treating them as required ceremony.

A failed attempt is useful when it provides new evidence. Retry or change approach when there is a plausible path to progress; when attempts stop yielding information, identify the missing decision, resource, or capability and work on something independent. Record what would unblock the item so a resumed session does not repeat the same dead end. Recheck blockers when their inputs change.

## Make acceptance mean something

Check off a DOD item only when its expected outcome is demonstrated. Record the command and result, repeatable user procedure and observed result, or explicit human acceptance with reviewer and outcome. Reference large logs or artifacts rather than burying the current state in raw output. A file's existence or an unperformed check does not prove its behavior.

Match verification to the change's impact and the agreed acceptance basis. Run relevant checks while working and required regression before milestone acceptance or completion. Passing earlier checks is insufficient when later changes invalidate their evidence: reopen affected items and obtain fresh evidence. Failed, skipped, or unavailable required checks leave acceptance pending; record the reason and affected work.

## Preserve enough state to resume

Maintain PROGRESS with the active goal, package path, current work, evidence, and blockers. Keep its summary consistent with DOD check-offs. Record meaningful decisions and results as they emerge; a handoff should expose what is true now and what can usefully happen next without requiring a replay of the conversation.

## Completion and blocked handoff

Declare **ALL DONE** only when every DOD item and global acceptance condition is satisfied for the final state, every VISION success criterion and user case is covered, required regression has passed, and required human acceptance is recorded. Include the final evidence references in PROGRESS.

If unresolved external prerequisites or user decisions block all remaining useful work, report **BLOCKED** with the affected items and exact input or action needed. A pause, failed verification, or blocked handoff is not completion. If the host ends the session earlier, record the actual state and next work without claiming either termination condition has been met.
</loop-template>
