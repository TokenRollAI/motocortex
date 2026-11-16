---
name: study-codebase
description: >-
  Study a repository from source and runtime evidence to explain its purpose,
  architecture, load-bearing dependencies, core mechanism, and transferable
  design trade-offs. Use when dissecting how an unfamiliar or open-source
  system actually works, preparing a deep technical study or learning Gist, or
  distilling a small implementation exercise around its central invariant. Do
  not use for routine code navigation, bug fixing, or architecture redesign.
---

Explain a codebase deeply enough that the reader can state its central invariant, predict how it behaves on edge cases, and build a minimal working version of its core mechanism. A folder inventory or pattern catalog explains nothing; optimize for a few load-bearing conclusions backed by causal traces.

## Pin the target and orient rapidly

Resolve repository URL, exact commit SHA, dirty/local state, and target subsystem from context, asking only when competing targets would waste the study. Default to the project's primary user-facing capability; in a large monorepo, map the macro topology briefly and bound deep tracing to the subsystem that delivers that capability.

Use an isolated checkout when fetching remote code, leaving the target repository untouched — a study never authorizes mutating source or running untrusted setup scripts. Orient in parallel via manifests, public entry points, configuration schemas, and high-signal integration tests; execute a focused example or test only when safe, authorized, and useful to resolve behavioral ambiguity.

## Trace causal mechanisms end-to-end

Treat READMEs and docs as claims to test against code, not ground truth. Pick one representative operation and trace it from public entry point through to durable state change or output:

- **Core mechanism**: identify the exact data representations, state transitions, scheduling/control loops, and invariants carrying the work — following causal responsibility across module or dependency boundaries rather than trusting directory names like `core/`.
- **Failure or boundary edge**: trace one revealing edge case (backpressure, partial failure, race, invalid input, recovery) that exposes *why* the mechanism is shaped as it is.
- **Boundaries and dependencies**: map state ownership and control flow (with a compact diagram only when it clarifies non-obvious topology), separating policy owned by this codebase from work delegated to libraries, runtimes, or external services. Distinguish runtime dependencies (pinned from manifests/lockfiles and verified at call sites) from build/test tooling, marking uninspected third-party internals explicitly.

Maintain strict epistemic hygiene in the prose itself: separate **inspected source**, **observed execution**, **documented intent**, and **inferred rationale**. Keep the main narrative readable without clicking a single link; reserve inline citations for surprising or subtle claims, and collect commit-pinned, descriptively labeled source links in a dependency-ordered reading appendix (falling back to honest local `path + symbol` pointers when no remote commit exists).

## Distill transferable trade-offs and a falsifiable mini-build

Reject generic praise ("clean", "modular", "scalable"). For each lesson worth keeping, name the **forcing constraint, concrete mechanism, capability bought, cost paid, and conditions under which the pattern transfers or breaks**.

Turn the single most instructive mechanism into a **proposed** small implementation exercise (implemented only if separately requested): strip away product chrome and peripheral infrastructure, preserve the core invariant, and specify concrete input -> output, minimum components, deliberate omissions, and an acceptance check whose boundary case would fail a naive imitation.

## Deliver a self-contained study and verify Gist publication

Write a standalone Markdown study in the user's language using [templates/STUDY.md](templates/STUDY.md), introducing components by role before symbol names and walking the concrete trace in connected prose. Save to the user's chosen path or an artifact directory outside the studied checkout without clobbering unrelated notes.

When the request includes publishing a GitHub Gist, treat that request as authorization for the scoped upload without a redundant confirmation gate, and follow [references/gist-publishing.md](references/gist-publishing.md) to verify uploaded raw content and visibility (defaulting to `secret` unless `--public` was requested). If auth or tooling blocks upload, preserve the finished local note and report the exact blocker — never pass off a local file as a published Gist.

## Done when

The study explains purpose, architecture, key dependencies, end-to-end core mechanism (including a revealing edge case), and costed design lessons in self-contained prose; epistemic status (`inspected`, `executed`, `documented`, `inferred`) stays explicit; commit-pinned evidence forms a usable reading route in the appendix; the proposed mini-build tests the core invariant; and any requested Gist is verified byte-for-byte with its visibility confirmed or its blocker stated plainly.
