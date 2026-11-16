# DOR template

Record discovered technical facts and concrete readiness gaps. Omit inapplicable sections; link every gap to the exact `DOD` items it blocks.

<dor-template>
# DOR (Definition of Ready)

## Settled context and assumptions

<Decisions locked in DECISIONS.md, reversible working assumptions in force, and open user decisions with gated work.>

## Technical baseline

<Verified stack, architectural boundaries, existing conventions to reuse, and working build/test/runtime commands.>

## External prerequisites

<Services, credentials (locations only, never secret values), fixtures, or environments required and their current availability.>

## Verification surfaces

<Runnable test suites, CLI/API harnesses, live browser tooling (ego-lite preferred when available), or human review channels — plus any missing verification capability.>

## Blockers

<Each unresolved prerequisite, gated DOD IDs, and exact unblocking input; write `None` when ready.>
</dor-template>
