---
name: agent-orchestration
description: >-
  Coordinate or execute multi-agent work across a Coordinator (Master) and
  focused Workers to align on and deliver user intent fast without coordination
  bloat. Use when delegation is authorized and you are deciding whether to split
  work, packaging shared context and contracts for subagents, Herdr (`hc`)
  terminals, or agent teams, resolving mid-flight worker escalations, pacing
  functional checks versus stage-end reviews, or executing a delegated worker
  brief. Do not use when the user prohibits subagents or when self-contained
  single-agent execution is faster than handoff overhead.
---

Multi-agent work exists to **land the user's real intent faster across genuinely independent slices** — never to multiply handoff ceremony, review ping-pong, or defensive code. Identify your active role from the prompt and session context first — **Coordinator (Master)** or **Worker** — and honor the user's delegation, read/write, and merge boundaries throughout. A worker executes its assigned slice without spawning further agents unless its brief explicitly authorizes sub-delegation.

## Coordinator: verify authorization, lock intent, and share context once

Confirm first that the request and host authorize delegation; when delegation is prohibited, read-only, or small and tightly coupled, execute directly. When authorized, use the fewest workers that cover genuinely independent subsystem or file-ownership seams. When one slice defines an interface another consumes (such as backend RPC shape -> frontend UI), freeze or stub that contract before launching downstream consumers.

Gather shared context **once** before dispatching: inspect `AGENTS.md` / `CLAUDE.md`, project docs (`llmdoc` when present), real product entry points, baseline branch/worktree paths, and shared runtime bottlenecks (such as a single local test database, tmpfs, or port). Frame every slice around **observable user or caller behavior** — who enters through which real surface, performs what action, and observes what end-to-end result (including write -> read-back consistency) — separating user-confirmed rules from reversible working assumptions.

When building from scratch or introducing a moderately complex UI/UX interaction, assign **one owner** to align on a playable visual demo first, then pass the reviewed demo and settled behavior into downstream briefs so workers do not duplicate demos; dispatch routine or settled slices straight to their assigned work. Carry verbatim user constraints and non-goals into [templates/WORKER-BRIEF.md](templates/WORKER-BRIEF.md) and operate `hc`, subagent, or worktree channels per [references/dispatch-channels.md](references/dispatch-channels.md).

## Worker: deliver the slice and verify real behavior without bloat

Confirm your workspace/worktree, baseline branch, allowed write paths, and referenced inputs before acting. Close read-only investigation or audit briefs with source-backed findings; for implementation briefs, build the agreed behavior directly (creating an upfront demo only when your brief explicitly assigns that demo) and verify **end-to-end functional behavior** on the real caller or product entry point. Follow existing repository conventions and enforce invariants once at the owning boundary rather than stacking per-layer defensive guards, speculative fallback branches, or single-use abstractions.

Keep verification proportional to your blast radius: exercise the live UI/CLI flow, write -> read-back path, targeted reproducer, and directly affected checks rather than authoring sprawling mock-heavy unit-test matrices or repeatedly running slow full-repository suites across rounds. Separate pre-existing unrelated baseline failures from your own changes once with evidence instead of chasing out-of-scope red checks.

## Escalate uncertainty to Coordinator; resolve forks without polling

As **Worker**, investigate discoverable repository facts yourself and complete pre-authorized mechanical wiring inside your assigned scope. Whenever instructions conflict (such as a brief clashing with a stated user rule), required inputs are missing, a fix crosses into another worker's files or shared contract, scope would expand, or an acceptance gate is skewed by environment load, report back immediately via [templates/WORKER-REPORT.md](templates/WORKER-REPORT.md) while continuing orthogonal unblocked work — never guess product semantics, silently relax acceptance criteria, or bypass the Coordinator to question the user directly.

As **Coordinator**, wait on push reports or lifecycle events (`hc wait --children any`, subagent completion, durable mail, or agreed report files checked on worker events) instead of polling worker screens in `read` loops. Resolve reversible technical choices and cross-worker contract questions yourself — recording updates once at the source and notifying affected workers — and bring a concrete fork to the user when only they can supply a missing input or authorize a change to visible behavior, scope, acceptance criteria, external contracts, security/data boundaries, or irreversible commitments.

## Check functionality per slice; scale review to stage integration

Verify each completed worker output against its agreed deliverable: confirm real entry-point behavior and file/contract boundaries for code slices, or evidence quality for investigation slices. Check upstream shared contracts (`core`, schema, RPC shape) immediately before downstream workers build on them.

Defer heavyweight architectural/code review until substantial slices consolidate rather than churning workers over style nits or hypothetical edge cases on every turn. Integrate within authorized merge rules, run regressions proportional to the combined blast radius and required goal gates, and send back only defects that break functionality or violate the agreed acceptance contract (handing off directly when the user reserved final acceptance).

## Done when

**Coordinator**: Delegation honors host/user authorization and matches real coupling; any greenfield or complex UI/UX demo is owned once and passed cleanly to implementers; briefs separate verified context, verbatim user rules, and slice ownership; mid-flight worker forks are settled without terminal-polling loops or avoidable user prompts; integrated work satisfies end-to-end functional checks and applicable acceptance gates without scope creep; and temporary helper sessions are cleaned up. **Worker**: The assigned investigation or implementation slice reaches its agreed functional proof within owned boundaries, free of speculative defensive layers or unit-test churn; every contract conflict, missing input, or cross-boundary fork is escalated promptly to the Coordinator; and status is delivered via [templates/WORKER-REPORT.md](templates/WORKER-REPORT.md) separating observed proof from pre-existing baseline state.
