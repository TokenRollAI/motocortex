# DOD template

Use this skeleton for verifiable acceptance. Organize items into milestones when useful, with ordering based on actual dependencies. Each item states an expected result and the evidence that can establish it.

<dod-template>
# DOD (Definition of Done)

## Acceptance basis

VISION.md describes the agreed outcomes. A checked item requires evidence for the current state: a command and result, a repeatable user procedure and observed result, or explicit human review with reviewer and outcome. Link the evidence from PROGRESS.md. Reopen items when later changes invalidate their evidence.

## Global acceptance

<Conditions applying to the complete result, including required regression checks, expected results, and any human acceptance. Every condition must be satisfied before completion.>

## Acceptance items

- [ ] <Item ID>: <observable outcome; VISION criterion or case covered; verification method and expected result; actual prerequisites, if any>

## End-to-end acceptance

- [ ] <Acceptance ID>: <complete user scenario or related scenarios; VISION case identifiers; command, repeatable procedure, or human review; expected outcome>

## Coverage

<Map every VISION success criterion and user case to acceptance items. One check may cover several outcomes when its evidence actually demonstrates each of them.>
</dod-template>
