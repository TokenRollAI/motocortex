# Interaction Specification Template

Write in the user's language, scoping strictly to touched flows and omitting inapplicable sections. Reference existing design-system components by name; for CLIs, swap visual/responsive sections for stream routing, exit codes, `--json` contracts, and TTY vs non-TTY behavior. Keep unresolved decisions explicit rather than papering over them with guesses.

<interaction-spec-template>
# [Feature or Surface]: Interaction Specification

[Scope, target platforms, reused design-system conventions, and related existing flows]

## Users, jobs, and accelerators

- Personas & frequency: [who operates this, how often, expertise range]
- Primary job & failure cost: [outcome required and blast radius of mistakes]
- Expert path: [shortcuts, command palette, bulk ops, URL/CLI/API automation]

## Domain objects and navigation

[User-facing objects, canonical terms, URL/state persistence, and how each view answers where-am-I / what-is-here / what-next.]

## Flows and state preservation

[Entry -> steps -> landing state for each touched flow, specifying what survives errors, reloads, and Back navigation (drafts, filters, selection, scroll).]

## Action state machines

| Action | Immediate signifier | Pending | Success | Definite failure | Unknown / timeout | Reversibility & backend support |
|---|---|---|---|---|---|---|
| [verb + object] | [ack] | [local lock & indicator] | [in-place feedback] | [inline error & preserved input] | [reconcile rule / idempotency] | [undo, preview/diff, or named confirm] |

## View states

[Behavior across reachable states: first-use, empty, loading, partial, full, slow, offline, permission-denied, partial-failure.]

## Safeguards, density, craft, and accessibility

- Subtraction & anti-bloat: [controls/options kept out of the primary viewport, command/drawer indexing, opinionated defaults chosen]
- Density & anti-slop craft: [Operate vs Onboard density target, calm chrome vs semantic status color, specific outcome verbs]
- Destructive / external side effects: [blast radius, undo vs named confirmation, agent approval/takeover gates]
- Microcopy & i18n: [canonical labels, inline error phrasing, text-expansion/locale rules]
- Accessibility & input modes: [semantic elements, focus order, full keyboard path, live announcements, single-pointer non-drag path, target sizing, reduced motion]
- Responsive / AI behavior (if applicable): [viewport adaptation; provenance, object-landed output, and local AI repair]

## Principle trade-offs and open forks

[Explicit choices made where heuristics collided, plus unresolved user/stakeholder decisions and what each blocks.]

## Live verification checklist

- [Cold primary path + keyboard-only completion]
- [Empty, slow, definite-error, and unknown-timeout recovery with zero data loss]
- [Destructive undo or named-consequence confirmation verified]
</interaction-spec-template>
