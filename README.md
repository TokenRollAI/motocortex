# motocortex

> all skill you need for agent coding.

**motocortex is [TokenRoll](https://github.com/TokenRollAI)'s general-purpose skill/plugin for development.** It is not tied to any one product — drop it into any repo to turn a rough idea into a set of documents an autonomous agent can run on its own.

Read in another language: [简体中文](./README.zh-CN.md)

## What it does

You run one command, `/start`, and it walks you through the setup: it reads the current state of your project, interviews you about the decisions you may not realize are still open, and lands five documents — `VISION.md` / `DOR.md` / `DOD.md` / `LOOP.md` / `PROGRESS.md`. After that, `/goal` drives the repo round after round: an agent picks an unchecked item, verifies it with reproducible evidence, checks it off, and keeps going until everything is done or only blockers remain.

## Flow

```
/start                                   ← authoring phase: the one command to remember
  1. gather context   (read the repo, existing conventions, the settled stack)
  2. /grill           ← interview until nothing is silently assumed → land DECISIONS.md
  3. /frame           ← produce VISION.md (what to build) + DOR.md (readiness risk list)
  4. /loop            ← from the goal, generate DOD.md (what counts as done)
                        + LOOP.md (how each round runs) + PROGRESS.md (the ledger)

/goal                                    ← execution phase: drive the repo autonomously
  run the LOOP state machine round by round: pick a DoD item → verify with
  reproducible evidence → check it off, until everything's done or only blockers
  remain (not installed as a command? paste the "How to start" block at the top
  of LOOP.md into any agent session)
```

## Skills

| skill | invocation | responsibility | artifacts |
|---|---|---|---|
| `start` | user | orchestration entry: chains the steps below | all five documents |
| `grill` | model | gather context + interview for the unasked questions until the frontier is empty | `DECISIONS.md` |
| `frame` | model | synthesize DECISIONS into the source of truth and the readiness list | `VISION.md` `DOR.md` |
| `loop` | model | generate the autonomous execution engine from the goal | `DOD.md` `LOOP.md` `PROGRESS.md` |
| `goal` | user | drive a prepared repo through the LOOP state machine to done or blockers | appends `PROGRESS.md` |

Two layers: `start`/`goal` handle **orchestration** (user-invoked), while `grill`/`frame`/`loop` are **reusable discipline** (pulled in by `start`).

## Design principles

- **Look up facts, leave decisions to the user.** Anything discoverable from the environment gets looked up, not asked. Real judgment calls go to you — one at a time, each with a recommended answer.
- **Don't re-litigate what's settled.** An existing mature stack or convention is recorded and confirmed, not re-interviewed.
- **Checking off means evidence.** Every DoD item is checked off on reproducible evidence — a command and its output, not "I think it's done."

## Install

As a Claude plugin (v0.0.1):

```
/plugin marketplace add TokenRollAI/motocortex
/plugin install motocortex
```

Or symlink the directories under `skills/` into your skills directory (e.g. `~/.claude/skills`).

### Other runtimes (Codex / OpenCode / Cursor / Antigravity / pi)

Each runtime's format is already generated and committed — clone and use it, no acplugin needed. Point your runtime at the matching directory:

| runtime | entry / skills dir |
|---|---|
| Codex | `.codex-plugin/plugin.json` (skills under `.agents/skills/`) |
| Antigravity | `.agents/` (`.agents/plugins/marketplace.json`) |
| Cursor | `.cursor-plugin/` + top-level `skills/` |
| OpenCode | `.opencode/skills/` |
| pi | `.pi/skills/` |

These are [acplugin](https://github.com/tokenRollAI/acplugin) mirrors generated from `skills/` + `.claude-plugin/` — don't edit them by hand.

#### Codex CLI

Codex reads skills from `.agents/skills/` — repo-level (`$CWD` up to repo root) and user-level (`$HOME/.agents/skills`), and it follows symlinks. So you have two options:

- **Per repo (zero config):** clone motocortex into your project (or add it as a submodule) so `.agents/skills/` sits at or above where you launch Codex. Codex discovers the five skills automatically; restart Codex if they don't show up.
- **Globally (all repos):** symlink the generated skills into your home folder.

  ```
  mkdir -p ~/.agents/skills
  ln -s "$(pwd)"/.agents/skills/* ~/.agents/skills/
  ```

Both are backed by [Codex's skill discovery](https://developers.openai.com/codex/skills). To disable one without deleting it, add a `[[skills.config]]` entry in `~/.codex/config.toml`.
