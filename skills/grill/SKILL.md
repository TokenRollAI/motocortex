---
name: grill
description: >-
  Clarify consequential open decisions through targeted codebase discovery and a
  focused user interview, recording settled choices and assumptions in
  DECISIONS.md. Use when ambiguous scope, conflicting requirements, unresolved
  acceptance criteria, or costly one-way commitments block confident execution.
  Do not use for discoverable repository facts or reversible local
  implementation details.
---

Resolve the uncertainty that would redirect the outcome or force expensive rework, then get out of the way. Clarification exists to unlock high-confidence execution, not to interrogate every hypothetical future branch.

## Exhaust discoverable facts before asking

Inspect the codebase, schemas, configuration, git history, docs, and any existing `DECISIONS.md` in parallel before formulating a single question; incorporate context already passed by the caller. Never ask the user what the repository or environment can answer directly. When a critical fact cannot be verified from available sources, surface that exact blind spot instead of silently guessing.

Separate verified facts, settled user decisions, reversible working assumptions, and genuinely open forks. Treat prior settled decisions as binding unless new evidence or the user's current request reopens them.

## Ask only one-way doors and user-owned trade-offs

Triage remaining unknowns by reversibility and ownership:

- **Decide and record** ordinary two-way implementation details that fit existing intent and conventions; log them as explicit working assumptions with what would invalidate them, and keep moving.
- **Ask the user** when the answer changes user-visible behavior, scope, acceptance criteria, external contracts, security/data boundaries, or commitments costly to reverse.

Frame every question as a concrete fork rather than an open-ended prompt: state why the choice matters to current work, lead with a recommended option and the cost it accepts, and contrast viable alternatives briefly. Ask one fork at a time when its answer prunes or reshapes downstream questions; group orthogonal questions only when doing so cuts round-trips without obscuring trade-offs. Use the host's structured question tool for crisp choices, or direct prose when nuance requires it.

If the user is unavailable, advance independent work under recorded reversible assumptions and hold only the paths gated on user-owned commitments; silence never authorizes scope changes or one-way bets.

## Persist decisions incrementally and stop early

Maintain `DECISIONS.md` incrementally using [templates/DECISIONS.md](templates/DECISIONS.md) inside the active goal directory (or the repository's established location) without clobbering unrelated records. Writing decisions as they land prevents context resets from re-litigating settled ground, and an explicit user answer needs no second confirmation ceremony.

## Done when

Authorized next work has an unambiguous outcome and acceptance contract; `DECISIONS.md` cleanly separates verified facts, settled decisions, reversible assumptions, and deferred questions mapped to the work they gate; and questioning stops the moment remaining answers would no longer change current execution. If a blocking user decision remains open, hand off that exact fork rather than claiming alignment.
