# PROGRESS template

Keep the live summary scannable in seconds; append concise, evidence-linked deltas below as meaningful state changes occur.

<progress-template>
# PROGRESS (execution ledger)

## Current state

- Goal: <active goal>
- Package: <path relative to repository root>
- Status: <ready | in_progress | blocked | complete>
- Active focus: <current slice or milestone>
- Verified DOD: <satisfied IDs with short evidence pointers; invalidated or pending IDs>
- Blockers: <unresolved gap -> gated IDs -> required input, or `None`>
- Next move: <highest-leverage unblocked action or exact unblock request>

## Log

### <Timestamp or increment>

- Changed: <what moved and why>
- Verified: <DOD IDs, command/procedure run on current revision, observed outcome, artifact path>
- Decisions: <new choices or assumption updates; link `DECISIONS.md`>
- Open: <remaining items, reopened checks, or blockers>
</progress-template>
