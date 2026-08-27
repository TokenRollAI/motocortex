# motocortex

> Agent skills for turning rough goals into executable plans—and brittle prompts into reliable contracts.

**motocortex is a skills-only collection for agent-driven development.** Its six composable skills help you clarify an idea, frame a verifiable project, generate an autonomous execution loop, drive that loop to completion, or improve a prompt without locking you into one agent or runtime.

Read in another language: [简体中文](./README.zh-CN.md)

## Quick start

Install from GitHub with the open [`skills` CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add TokenRollAI/motocortex
```

The installer discovers the `SKILL.md` files directly, then lets you choose the skills, target agents, and installation scope. No motocortex package or runtime-specific adapter is required.

Useful variants:

```bash
# Preview the six available skills
npx skills add TokenRollAI/motocortex --list

# Install only the orchestration skills
npx skills add TokenRollAI/motocortex --skill start --skill goal

# Install for your user account instead of the current project
npx skills add TokenRollAI/motocortex --global
```

## Workflows

motocortex has two independent paths:

```text
rough project goal
└── start
    ├── grill  → DECISIONS.md
    ├── frame  → VISION.md + DOR.md
    └── loop   → DOD.md + LOOP.md + PROGRESS.md

prepared project
└── goal       → run the LOOP state machine until done or blocked

rough or existing prompt
└── better-prompt → copy-ready prompt + runtime notes + minimal evals
```

`DECISIONS.md` preserves the clarification handoff. The five execution documents—`VISION.md`, `DOR.md`, `DOD.md`, `LOOP.md`, and `PROGRESS.md`—form the package another agent can pick up and run.

## Skills

| skill | invocation | responsibility | artifacts |
|---|---|---|---|
| `start` | user | orchestrate goal clarification, framing, and loop generation | all five execution documents |
| `grill` | model | inspect context and settle every material open decision | `DECISIONS.md` |
| `frame` | model | turn settled decisions into the source of truth and readiness risks | `VISION.md`, `DOR.md` |
| `loop` | model | turn the goal into a verifiable autonomous execution engine | `DOD.md`, `LOOP.md`, `PROGRESS.md` |
| `goal` | user | drive a prepared repository through the loop to done or blockers | updates `PROGRESS.md` |
| `better-prompt` | model | draft, diagnose, or optimize prompts with focused domain guidance | optimized prompt, runtime notes, minimal evals |

`start` and `goal` are user-invoked orchestration skills. `grill`, `frame`, and `loop` are reusable disciplines composed by `start`; `better-prompt` activates independently when the prompt itself is the artifact or problem.

## How to use it

After installation, ask your agent to use `start` with a rough project goal:

```text
Use start to turn this goal into an autonomous execution plan: <your goal>
```

Some hosts expose user-invoked skills as slash commands, so the same action may appear as `/start`. Answer the decision questions, review the generated documents, then invoke `goal` to execute them:

```text
Use goal to drive this repository until the definition of done is complete or only blockers remain.
```

For prompt work, give `better-prompt` either a rough intent or an existing prompt. It loads only the domain guidance relevant to that task instead of expanding every prompt into one universal template.

## Design principles

- **Look up facts; leave decisions to the user.** Discoverable context is inspected. Material judgment calls are surfaced one at a time with a recommendation.
- **Do not re-litigate settled choices.** Existing stacks and conventions are recorded and reused.
- **Checking off means evidence.** Every definition-of-done item requires a reproducible command or user case, not a confidence statement.
- **Prompts are contracts, not incantations.** Keep the portable core lean, add guidance only when it changes behavior, and validate it on representative cases.
- **Files carry state.** Decisions, readiness risks, completion criteria, execution rules, and progress survive across agents and context windows.

## Repository structure

```text
skills/
├── start/
├── grill/
├── frame/
├── loop/
├── goal/
└── better-prompt/
```

`skills/` is the only distribution source of truth. Each skill keeps its decision-making discipline in `SKILL.md` and puts copyable artifact skeletons under its own `templates/` directory.

When adding or removing a skill, update the skills tables in both READMEs and verify discovery locally:

```bash
npx -y skills add . --list
```
