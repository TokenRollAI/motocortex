# DOR template

When producing `DOR.md`, copy this skeleton. Turn every line into a concrete item for this project — leave no placeholder text. Check off what is satisfied; mark what is missing as a blocker.

<dor-template>
# DOR (Definition of Ready)

> Readiness-risk list before work starts. Satisfied items are checked off.
> Unsatisfied items do not block the start — they are inherited into PROGRESS
> as blockers, narrowing what the agent can advance this run (DoD items that
> depend on them get skipped) instead of stalling the whole effort. The point
> is to start running with a clear picture of what is not ready, not to wait
> at the gate.

## Requirements readiness
- [ ] Every VISION success criterion is verifiable (checkable by a command or a user case)
- [ ] No silent assumptions (every assumption grill recorded has been ratified by the user)

## Technical readiness
- [ ] Technology stack settled (existing choices recorded; new choices justified)
- [ ] Build / test / run commands known and runnable

## External prerequisites
- [ ] Required credentials / accounts / external services in place (list each; mark missing ones as blockers)
- [ ] Upstream dependencies / environments reachable

## Acceptance readiness
- [ ] Every user case has a re-runnable acceptance command that can be written for it

## Blockers
<List every unsatisfied prerequisite here; the engine step copies them into
 PROGRESS's initial state. Write "none" if there are none.>
</dor-template>
