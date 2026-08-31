# DOD template

When producing `DOD.md`, copy this skeleton. The number and content of phases depend on the project; the final phase is always E2E and maps to every user case in VISION.

<dod-template>
# DOD (Definition of Done)

> Check-off discipline: an item may be checked if and only if there is a
> re-runnable command whose output proves it. "I think it's done" does not
> count. The source of truth for the spec is VISION.md.

## Global definition of done

The project is done when all of the following hold:
1. Every phase's DoD list is fully checked, each item backed by a re-runnable command.
2. Every E2E item in the final phase passes (one per VISION user case).
3. <Project-specific global conditions, e.g. "one-command build is green".>

## Phase 0 — <name>

**Goal**: <what exists when this phase ends>
**DoD**:
- [ ] <verifiable item, with the command that verifies it>
- [ ] ...

## Phase 1 — <name>

**Goal**: ...
**DoD**:
- [ ] ...

## Phase N — E2E acceptance

> Each E2E item maps to one VISION user case — scripted and re-runnable.
> Checkboxes carry the state; the check-off discipline at the top applies.

- [ ] **E2E-1** <Case 1>: <re-runnable command + expected output>
- [ ] **E2E-2** <Case 2>: ...
</dod-template>
