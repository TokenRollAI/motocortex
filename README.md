# motocortex

> TokenRollAI's in-house agent skills: clarify consequential choices, carry goals to verified completion, and explain the judgment behind architecture, performance, and prompt decisions.

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
| `start-a-goal` | user | carry a goal to verified completion with resumable execution documents and evidence | `VISION.md`, `DOR.md`, `DOD.md`, `LOOP.md`, `PROGRESS.md` |
| `grill` | model | resolve consequential open decisions and record assumptions and deferred questions | `DECISIONS.md` |
| `architecture-design` | model | design or review architecture, technology choices, boundaries, and evolution without speculative complexity | task-adapted decision, design, or review |
| `performance-optimization` | model | design, diagnose, optimize, or review performance from workload goals and evidence | task-adapted strategy, diagnosis, or verified change |
| `better-prompt` | model | draft, diagnose, or optimize prompts with focused domain guidance | optimized prompt, runtime notes, minimal evals |

`start-a-goal` is the single user-invoked entry point. The other four are model-invoked disciplines: `grill` is used by `start-a-goal` when consequential decisions need clarification and also stands alone when uncertainty prevents useful progress; `architecture-design`, `performance-optimization`, and `better-prompt` are independent — the model selects them from their descriptions when a task genuinely needs them, and they do not call or depend on one another.

## How start-a-goal works

```text
current goal
└── start-a-goal
    ├── reconcile intent and existing execution state
    ├── clarify consequential choices as needed → grill → DECISIONS.md
    ├── maintain the package → VISION + DOR + DOD + LOOP + PROGRESS
    └── advance authorized work → verify outcomes or expose blockers
```

Existing documents are checked against the current goal and project state before reuse. Matching packages resume; missing or stale documents are repaired from supported decisions, and unrelated goals stay in separate directories. The five execution documents preserve `VISION.md` (outcomes and scope), `DOR.md` (readiness gaps and dependencies), `DOD.md` (acceptance and evidence), `LOOP.md` (execution judgment and completion conditions), and `PROGRESS.md` (current state and evidence history).

These are responsibilities, not mandatory stages. The agent chooses work by actual dependencies and feedback, records decisions as they emerge, and verifies outcomes with commands, repeatable user procedures, or explicit human acceptance. Required regression must pass for the final state before completion; a blocked handoff remains unfinished work.

## How to use it

After installation, hand your agent a rough goal:

```text
Use start-a-goal to take this to done: <your goal>
```

Some hosts expose user-invoked skills as slash commands, so the same action may appear as `/start-a-goal`. Answer consequential clarification questions when needed and let the agent carry the goal forward. Existing decisions and authorization are reused. If the host ends execution before completion, resume through its supported continuation mechanism; the package preserves the current state.

The model-invoked disciplines trigger on their own when a task matches their descriptions, or on request:

```text
Use grill to settle the decisions that matter before we commit to this idea.

Review this service boundary and recommend the simplest architecture that meets these quality requirements.

Diagnose this latency regression, establish a representative baseline, and keep only improvements the evidence supports.

Rewrite this prompt around intent, reasons, and judgment; give me concrete checks for whether behavior improves.
```

## Design principles

- **Explain why; leave room for judgment.** State intent, causal trade-offs, and observable completion. Fix a procedure only when its order is required for correctness, authorization, reproducibility, or the user's chosen process.
- **Look up facts; surface consequential choices.** Inspect relevant context and ask where the answer changes the work. Handle ordinary reversible choices within existing intent and authorization.
- **Do not re-litigate settled choices.** Existing stacks and conventions are recorded and reused.
- **Checking off means evidence.** Acceptance requires observed results from a command, repeatable user procedure, or explicit human review. Failed required regression prevents completion; weakening the goal cannot make an implementation correct.
- **Architecture starts with forces, not patterns.** Business outcomes, quality scenarios, constraints, and credible change determine structure and technology; every layer and extension point must pay for itself.
- **Performance is behavior under load.** Define the workload and target, find the real constraint, then choose the transformation whose trade-offs fit the evidence.
- **Prompts are contracts, not incantations.** Keep the portable core lean, add guidance only when it changes behavior, and validate it on representative cases.
- **Files carry state.** Decisions, readiness risks, completion criteria, execution rules, and progress survive across agents and context windows.

## Repository structure

```text
skills/
├── start-a-goal/
│   ├── SKILL.md      # goal ownership and execution judgment
│   └── templates/    # VISION, DOR, DOD, LOOP, PROGRESS skeletons
├── grill/
│   └── templates/    # durable decision record
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
