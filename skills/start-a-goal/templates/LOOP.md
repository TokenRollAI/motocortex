# LOOP template

When producing `LOOP.md`, copy this skeleton almost verbatim. It is the execution contract an autonomous agent reads every round; the content is project-independent unless this project needs extra discipline.

<loop-template>
# LOOP (continuous execution contract)

> This file pairs with DOD.md: DOD defines what counts as done, this file
> defines how each round runs. It is an unattended (AFK) contract: no human
> reviews between rounds, so the evidence gate, promotion, and termination
> conditions are hard-coded below.

## How to launch

Paste the following into an agent session (or invoke `start-a-goal` if it is installed as a command — it drives from here automatically):

```
Read this repository's LOOP.md and PROGRESS.md, then run LOOP.md's state
machine round after round until a termination condition is hit. At the end
of every round, write the evidence and check-offs into PROGRESS.md.
You are authorized to edit files autonomously; judge commits and other
outward actions by LOOP's discipline and the host's conventions.
```

How many rounds run per invocation depends on the host: some harnesses run one round per reply, in which case re-enter repeatedly (a manual "continue", a script, or an outer loop). This file only guarantees that whoever wakes the loop, behavior is identical — and it knows when to stop.

## Inviolable discipline
1. **DOD is the judge**: only reproducible evidence (command + output, or an equivalent re-runnable check) can check off a DoD item. Not run, no evidence — no check.
2. **Never fake progress**: report failures as failures; declare skips as skips.
3. **The spec is the constitution**: when the implementation diverges from VISION or the documents, update the document with the reason first, then write the code.
4. **Mature frameworks first**: about to build a wheel from scratch — stop and look for an existing one.

## Adapt to host capabilities (judgment, not orders)
- **Commits**: default to small, frequent commits — but first check that the working tree is clean and the user has authorized committing. Without authorization, keep the changes, note them in PROGRESS, and do not commit on your own.
- **Subagents**: farm out cleanly-bounded subtasks to parallel subagents for speed; if the host lacks them, do the work sequentially yourself.
- **Regression**: every round, run the checks relevant to the current item; run the full regression each round if it is cheap, otherwise once at each phase promotion.

## Every round
1. Get context: read PROGRESS.md (current phase, leftovers, blockers) + the current phase in DOD.
2. Pick the target: one unchecked DoD item in the current phase that no blocker holds up — the round's single goal.
3. Implement: see "Adapt to host capabilities".
4. Verify: obtain the item's reproducible evidence. Paste the command and output into PROGRESS, then check the DoD item.
5. Record: update PROGRESS; write down any traps hit so the next round avoids them.

## State machine: promotion and termination
At the end of each round, decide the next step:
- **Phase promotion**: every DoD item in the current phase checked (for the E2E phase: every E2E item checked) → run the phase's full regression once, evidence into PROGRESS → move to the next phase. Never skip phases.
- **All done (terminate)**: the final (E2E) phase fully checked → write "ALL DONE" with the final evidence at the top of PROGRESS and stop.
- **Stuck — skip**: the same DoD item fails to close for 3 consecutive rounds, or hits a decision only a human can make → mark it as a blocker in PROGRESS and move to the next workable item. Do not idle, do not burn tokens grinding a stuck point.
- **Phase deadlocked (terminate)**: every remaining unchecked item in the current phase is blocked and nothing can advance → stop, leave the blocker list at the top of PROGRESS for the human. Do not jump to later phases to route around a blocked prerequisite.

## Per-round output format (append to PROGRESS.md)
```
## Round <N> — <date>
- Target: <phase X / DoD item verbatim>
- Actions: <implementation summary; subagents dispatched and their conclusions>
- Verification: <command → result> (one per line)
- Checked off: <DoD items checked / none>
- Leftovers: <blockers or the suggested starting point for the next round>
```
</loop-template>
