---
name: start-a-goal
description: >-
  Take a goal from rough idea to verified done — clarify it, generate the
  execution documents (VISION, DOR, DOD, LOOP, PROGRESS), then drive the loop
  round after round until everything is done or only blockers remain.
disable-model-invocation: true
---

You own the whole journey of a goal: turn it into a set of documents an autonomous agent can run without supervision, then be that agent. The documents — not your conversation memory — carry all state, so the work survives compaction, session restarts, and handoffs to other agents.

Extract the goal from what the user has already said. If no clear goal emerges, ask for it before doing anything else.

## Pick the mode

Check whether `VISION.md` / `DOR.md` / `DOD.md` / `LOOP.md` / `PROGRESS.md` already exist in the repository.

- **All five exist**: skip Setup and go straight to Drive (read `PROGRESS.md` to locate where things stand).
- **Some exist**: do not overwrite blindly — ask the user which way to go:
  - **Resume**: the documents are usable as-is; drive from where `PROGRESS.md` left off.
  - **Revise**: the goal changed; merge the new conclusions into the existing documents instead of rewriting them.
  - **Fresh start**: write the new set to a namespaced path (such as `<slug>/VISION.md`) or archive the old set first — never overwrite in place.
- **None exist**: run Setup, then Drive.

## Setup

Four steps in order, on one uninterrupted thread of thought — do not compact or clear context between them. (Automatic compaction is outside prompt control; if it happens midway, later steps must re-read the documents already on disk instead of trusting memory.)

1. **Gather context.** Read the project's current state: repository structure, existing conventions, the settled technology stack, README and existing docs. Sort the findings into two piles — settled and open. This output feeds directly into the next step; do not collect it twice.

2. **Clarify.** Run the `grill` skill with that context. It interrogates the user one decision at a time — including questions they may not realize are open — until nothing is silently assumed, and writes the conclusions to `DECISIONS.md`.

3. **Frame.** Write `VISION.md` and `DOR.md` from `DECISIONS.md`, following the framing discipline below. `DECISIONS.md` is the authoritative source — do not re-interview, and do not write from session memory alone.

4. **Build the engine.** Generate `DOD.md`, `LOOP.md`, and `PROGRESS.md` from the goal and `VISION.md`, following the engine discipline below.

When all five documents are on disk, tell the user the five file paths, then continue into Drive — or, if the user prefers to hand off, point them at the "How to launch" section at the top of `LOOP.md`, which any agent session can bootstrap from.

### Framing discipline (VISION + DOR)

Skeletons are in `templates/VISION.md` and `templates/DOR.md` — copy their structure and fill every section. Beyond the skeleton, the judgment calls:

- VISION says **what** to build, never how. Its two load-bearing parts feed DOD directly:
  - **Success criteria**: each one must be checkable by a single command or a single user case. Sharpen or delete any criterion that cannot be verified.
  - **User cases**: break the success criteria into concrete scenarios ("user does X → gets Y"). Each case later maps one-to-one to an E2E item in DOD.
- DOR is a **readiness-risk list**, not a hard gate. List the context inputs that should be ready before work starts, as concrete project-specific items. Check off what is satisfied; mark what is missing as a **blocker**. Blockers get inherited into PROGRESS and narrow what the agent can advance (items depending on them are skipped) — they do not halt the whole effort. An unlisted gap is a lost gap.
- Stack conclusions land in DOR's technical-readiness section: record and check off what is already settled; state the reason for anything newly chosen.

### Engine discipline (DOD + LOOP + PROGRESS)

Skeletons are in `templates/DOD.md`, `templates/LOOP.md`, and `templates/PROGRESS.md`. `LOOP.md` can be copied almost verbatim; `DOD.md` needs project-specific phases; `PROGRESS.md` is just initialization. The three roles must not blur: **DOD is the judge (what counts as done), LOOP is the foreman (how each round runs), PROGRESS is the ledger (where things stand).**

- Cut the project into **ordered phases** — each phase ends with something verifiable, and each builds on the previous. The final phase is E2E and must cover **every** user case in VISION, with none missing.
- Next to every DoD item, write the **re-runnable command that verifies it**. An item you cannot write a command for is still too vague — split or rewrite it.
- Copy every blocker from `DOR.md` into PROGRESS's initial state. That is the reality the first round faces; an uncopied blocker gets treated as ready.

## Drive

Read `LOOP.md` and `PROGRESS.md`, then run the state machine `LOOP.md` defines, round after round, until you hit its termination conditions:

- At the end of every round, write reproducible evidence (command + output) and check-offs into `PROGRESS.md`.
- You are authorized to edit files autonomously; judge commits and other outward actions by `LOOP.md`'s discipline and the host's conventions.
- All DoD items checked, including E2E → report completion.
- Only blockers remain and nothing can advance → leave the blocker list at the top of `PROGRESS.md` and stop for the user.

`LOOP.md` is the single authority — do not duplicate or override its rules here. If the host runs only one round per invocation, re-enter this skill to continue.

## Done when

Setup is done when the five documents are on disk and self-consistent: DOD's phases cover every VISION success criterion and user case, LOOP's round cycle points at DOD, and PROGRESS is initialized with DOR's blockers inherited. Drive is done when `LOOP.md`'s termination conditions say so — full completion with final evidence in PROGRESS, or a blocker list waiting for the user.
