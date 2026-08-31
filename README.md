# motocortex

> TokenRollAI's in-house agent skills: interrogate a rough goal until nothing is silently assumed, drive it to verified done, and make sound architecture, performance, and prompt decisions along the way.

**motocortex is the skills collection TokenRollAI builds for its own agent-driven development.** It is public and anyone is welcome to install it, but it encodes how we work rather than trying to serve every workflow: opinionated defaults, evidence-gated progress, and files — not conversation memory — carrying all state. Expect it to evolve with our practice, including breaking changes.

Read in another language: [简体中文](./README.zh-CN.md)

## Quick start

Install from GitHub with the open [`skills` CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add TokenRollAI/motocortex
```

The installer discovers the `SKILL.md` files directly, then lets you choose the skills, target agents, and installation scope. No package or runtime-specific adapter is required.

Useful variants:

```bash
# Preview the available skills
npx skills add TokenRollAI/motocortex --list

# Install for your user account instead of the current project
npx skills add TokenRollAI/motocortex --global
```

## Skills

| skill | invocation | responsibility | artifacts |
|---|---|---|---|
| `start-a-goal` | user | take a goal end to end: clarify it, generate the execution documents, then drive the loop until done or blocked | `VISION.md`, `DOR.md`, `DOD.md`, `LOOP.md`, `PROGRESS.md` |
| `grill` | model | inspect the context, then interview the user one decision at a time until nothing is silently assumed | `DECISIONS.md` |
| `architecture-design` | model | design or review architecture, technology choices, boundaries, and evolution without speculative complexity | task-adapted decision, design, or review |
| `performance-optimization` | model | design, diagnose, optimize, or review performance from workload goals and evidence | task-adapted strategy, diagnosis, or verified change |
| `better-prompt` | model | draft, diagnose, or optimize prompts with focused domain guidance | optimized prompt, runtime notes, minimal evals |

`start-a-goal` is the single user-invoked entry point. The other four are model-invoked disciplines: `grill` is pulled in by `start-a-goal` during clarification and also stands alone whenever a task is too vague to execute; `architecture-design`, `performance-optimization`, and `better-prompt` are independent — the model selects them from their descriptions when a task genuinely needs them, and they do not call or depend on one another.

## How start-a-goal works

```text
rough goal
└── start-a-goal
    ├── clarify → grill → DECISIONS.md
    ├── frame   → VISION.md + DOR.md
    ├── engine  → DOD.md + LOOP.md + PROGRESS.md
    └── drive   → run the LOOP state machine until done or only blockers remain
```

On a repository that already has the execution documents, `start-a-goal` skips generation and goes straight to driving. The five execution documents form a package any agent can pick up and run: `VISION.md` (what to build, success criteria), `DOR.md` (readiness risks), `DOD.md` (what counts as done), `LOOP.md` (how each round runs), and `PROGRESS.md` (the ledger).

## How to use it

After installation, hand your agent a rough goal:

```text
Use start-a-goal to take this to done: <your goal>
```

Some hosts expose user-invoked skills as slash commands, so the same action may appear as `/start-a-goal`. Answer the clarification questions, review the generated documents, and let the agent drive. Hosts that run one round per invocation need re-entry (a manual "continue", a script, or an outer loop) to reach the termination conditions.

The model-invoked disciplines trigger on their own when a task matches their descriptions, or on request:

```text
Use grill to pin down what's still open about this idea before we build anything.

Review this service boundary and recommend the simplest architecture that meets these quality requirements.

Diagnose this latency regression, establish a representative baseline, and keep only improvements the evidence supports.

Rewrite this prompt into a minimal task contract and give me the evals to prove it improved.
```

## Design principles

- **Look up facts; leave decisions to the user.** Discoverable context is inspected. Material judgment calls are surfaced one at a time with a recommendation.
- **Do not re-litigate settled choices.** Existing stacks and conventions are recorded and reused.
- **Checking off means evidence.** Every definition-of-done item requires a reproducible command or user case, not a confidence statement.
- **Architecture starts with forces, not patterns.** Business outcomes, quality scenarios, constraints, and credible change determine structure and technology; every layer and extension point must pay for itself.
- **Performance is behavior under load.** Define the workload and target, find the real constraint, then choose the transformation whose trade-offs fit the evidence.
- **Prompts are contracts, not incantations.** Keep the portable core lean, add guidance only when it changes behavior, and validate it on representative cases.
- **Files carry state.** Decisions, readiness risks, completion criteria, execution rules, and progress survive across agents and context windows.

## Repository structure

```text
skills/
├── start-a-goal/
│   ├── SKILL.md      # orchestration and driving discipline
│   └── templates/    # VISION, DOR, DOD, LOOP, PROGRESS skeletons
├── grill/
├── architecture-design/
├── performance-optimization/
└── better-prompt/
    ├── references/   # domain guides, model adaptation, evaluation
    └── templates/    # prompt delivery skeleton
```

`skills/` is the only distribution source of truth. Each skill keeps its decision-making discipline in `SKILL.md`, puts copyable artifact skeletons under `templates/`, and puts load-on-demand deep guidance under `references/`. All skill content is written in English.

When adding or removing a skill, update the skills tables in both READMEs and verify discovery locally:

```bash
npx -y skills add . --list
```
