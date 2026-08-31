# PROGRESS template

When producing `PROGRESS.md`, initialize it as this empty ledger. Copy the blockers from `DOR.md` one by one. The agent appends to it every round afterwards.

<progress-template>
# PROGRESS (execution ledger)

> Append one Round entry at the end after every round (format in LOOP.md).
> The current phase and blockers are maintained here.

## Current state
- Current phase: Phase 0
- Checked off: none
- Blockers: <inherit each item from DOR.md's Blockers section; write "none" if empty>

## Round log

<The agent appends one entry per round, newest last.>
</progress-template>
