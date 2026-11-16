# LOOP template

Tailor this execution contract to the goal's dependencies, verification surfaces, and host authorization. Keep `<goal-directory>` relative to the repository root so any resumed agent resolves the right package immediately.

<loop-template>
# LOOP (execution contract)

## Resume protocol

Read `<goal-directory>/LOOP.md` and `PROGRESS.md`, verify they match the active request and git/workspace state, then advance authorized work against `VISION.md` and `DOD.md`. This file records execution discipline; it grants no permissions beyond the host and user instructions.

## Scope and authority

Keep code and package docs aligned with current user intent. Fix code when it violates agreed outcomes; update stale package docs when verified repo facts or user instructions supersede them. Pause for user decision before altering user-owned scope, acceptance criteria, or irreversible commitments, while continuing orthogonal unblocked work.

## Stage cadence and execution strategy

Not every turn warrants a deep review. Drive work through a clear progression: **working demo / thin vertical slice -> implementation -> functional verification -> consolidating and merging major stage work -> deep architectural review** once real behavior and coupling pressures are proven in running code. Check one-way safety/contract boundaries before crossing them, keep turn-by-turn iteration fast and functional, and run deep structural review after major stage consolidation rather than policing every intermediate edit.

Combine tightly coupled items and parallelize independent discovery or verification where supported. Fix root causes at the owning boundary rather than silencing checks or patching symptoms. When retries stop producing new information, stop thrashing: isolate the missing fact, capability, or decision, record what blocks that path in `PROGRESS.md`, and pivot to independent unblocked work. Re-evaluate blockers whenever inputs change.

## Verification integrity

Check off `DOD` items only from observed results on the current state — command exit and output, repeatable live procedure (`ego-lite` preferred on web UIs when available), or recorded human acceptance. Later edits inside an item's blast radius invalidate prior check-offs until re-run. Link concise artifacts or logs from `PROGRESS.md` instead of pasting walls of output.

## Termination states

- **ALL DONE**: Every `DOD` item, end-to-end check, stage-end architectural review, and global regression/human gate passes on the final state, covering all `VISION` criteria and user cases, with final evidence recorded in `PROGRESS.md`.
- **BLOCKED**: All remaining useful work depends on missing external prerequisites or user decisions; report exact blockers and required inputs without claiming completion.
- **INTERRUPTED**: If the session ends mid-flight, leave `PROGRESS.md` accurate on current state, invalidated checks, and the next concrete move.
</loop-template>
