# motocortex

> Agent skills for turning rough goals into executable plans, making sound architecture and performance decisions, and turning brittle prompts into reliable contracts.

**motocortex is a skills-only collection for agent-driven development.** Its eight composable skills help you clarify an idea, frame and execute a verifiable project, make architecture and performance decisions, or improve a prompt without locking you into one agent or runtime.

Read in another language: [简体中文](./README.zh-CN.md)

## Quick start

Install from GitHub with the open [`skills` CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add TokenRollAI/motocortex
```

The installer discovers the `SKILL.md` files directly, then lets you choose the skills, target agents, and installation scope. No motocortex package or runtime-specific adapter is required.

Useful variants:

```bash
# Preview the eight available skills
npx skills add TokenRollAI/motocortex --list

# Install only the orchestration skills
npx skills add TokenRollAI/motocortex --skill start --skill goal

# Install for your user account instead of the current project
npx skills add TokenRollAI/motocortex --global
```

## Workflows

motocortex has five independent entry paths:

```text
rough project goal
└── start
    ├── grill  → DECISIONS.md
    ├── frame  → VISION.md + DOR.md
    └── loop   → DOD.md + LOOP.md + PROGRESS.md

prepared project
└── goal       → run the LOOP state machine until done or blocked

architecture decision, review, or evolution
└── architecture-design → justified structure, stack, boundaries, and trade-offs

performance goal, scale risk, or regression
└── performance-optimization → evidence-backed design, diagnosis, or optimization

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
| `architecture-design` | model | design or review architecture, technology choices, boundaries, and evolution without speculative complexity | task-adapted decision, design, or review |
| `performance-optimization` | model | design, diagnose, optimize, or review performance from workload goals and evidence | task-adapted strategy, diagnosis, or verified change |
| `better-prompt` | model | draft, diagnose, or optimize prompts with focused domain guidance | optimized prompt, runtime notes, minimal evals |

`start` and `goal` are user-invoked orchestration skills. `grill`, `frame`, and `loop` are reusable disciplines composed by `start`. `architecture-design`, `performance-optimization`, and `better-prompt` are independent model-invoked disciplines selected from their descriptions when the task genuinely needs them; they do not call or depend on one another.

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

Ask architecture questions directly when a system or major feature needs structural decisions, a technology choice, a review, or an evolution path:

```text
Review this service boundary and recommend the simplest architecture that meets these quality requirements.
```

Use performance work when there is a target, bottleneck signal, or credible scale risk. The skill distinguishes design-time workload reasoning from measurement of an existing system:

```text
Diagnose this latency regression, establish a representative baseline, and keep only improvements the evidence supports.
```

## Design principles

- **Look up facts; leave decisions to the user.** Discoverable context is inspected. Material judgment calls are surfaced one at a time with a recommendation.
- **Do not re-litigate settled choices.** Existing stacks and conventions are recorded and reused.
- **Checking off means evidence.** Every definition-of-done item requires a reproducible command or user case, not a confidence statement.
- **Architecture starts with forces, not patterns.** Let business outcomes, quality scenarios, constraints, existing context, and credible change determine structure and technology; every layer and extension point must pay for itself.
- **Performance is behavior under load.** Define the workload and target, find the real constraint, then choose async, batching, streaming, concurrency, caching, or local optimization only when their trade-offs fit the evidence.
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
├── architecture-design/
├── performance-optimization/
└── better-prompt/
```

`skills/` is the only distribution source of truth. Each skill keeps its decision-making discipline in `SKILL.md` and puts copyable artifact skeletons under its own `templates/` directory.

When adding or removing a skill, update the skills tables in both READMEs and verify discovery locally:

```bash
npx -y skills add . --list
```
