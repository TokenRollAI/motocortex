---
name: interaction-design
description: >-
  Design, review, or implement user-facing interaction and modern UI/UX craft
  from user goals, domain objects, empirical evidence, and complete action state
  lifecycles. Use when shaping how people discover, understand, execute, or
  recover from actions in a web or mobile app, desktop UI, data-heavy workspace,
  CLI, or AI/agent interface: information architecture, anti-bloat feature
  restraint, density calibration, navigation, forms, tables and search, async
  and unknown-outcome states, error recovery and undo, microcopy and
  localization, accelerators, accessibility, AI-slop elimination, or live UI
  dogfooding. Do not use for backend-only changes that leave user-visible
  states, flows, and density untouched.
---

Good interaction minimizes cognitive and physical cost: users see system state immediately, predict what an action will do, execute it fast, and recover cheaply when things fail. Modern UI/UX craft achieves this through **restraint, opinionated defaults, and subtraction** — never by stacking a new tab, toolbar button, card, or settings toggle onto the screen for every new feature.

Scope the work to the task. A review diagnoses concrete user, flow, density, and craft failures with convention-aligned fixes (including what to cut); a specification defines objects, states, and recovery completely enough to build; an implementation proves those states and ergonomics live in the running interface. Reuse existing design-system tokens, components, URL conventions, and domain terms before inventing anything, and ask the user only about forks that alter product behavior: target persona, acceptable risk, or speed-versus-safety trade-offs.

## Scale power without stacking UI

Anchor navigation, lists, search, and URLs on stable user-recognized objects — projects, issues, invoices, deployments — rather than backend services or join tables. Every view must answer *where am I, what is here, and what can I do next*, designed from user goal -> object model -> interaction pattern -> component state machine rather than outward from decorative chrome.

Hold interfaces to the restraint of modern category benchmarks rather than enterprise feature-stacking (read [references/modern-product-craft.md](references/modern-product-craft.md) when shaping layouts, auditing bloat, or reviewing UI craft):

- **Opinionated defaults + command-indexed depth (Linear)**: Commit to a clean default workflow instead of offloading indecision into sprawling settings; keep workspace chrome calm and monochrome so saturated color means real semantic state; keep primary rows dense and scannable while indexing secondary actions into `Cmd+K` and selection-aware menus instead of per-row button clutter.
- **Single-intent entry + progressive enabling + Undo (Google Search / Drive / Gmail)**: Lead with one unmistakable primary action, reveal filters or batch toolbars only after intent or selection justifies them, and execute routine reversible actions immediately with crisp Undo rather than nagging confirmation modals.
- **Flat primary surface + contextual inspectors (Stripe / Figma)**: Keep primary lists and canvases uncluttered; slide deep metadata into lateral drawers that preserve list context, and surface property controls strictly for the currently selected object type.

## Resolve competing principles explicitly

When heuristics collide, decide by **action frequency, consequence severity, true backend reversibility, and user expertise**, stating the trade-off chosen:

- **Convention vs novelty**: Depart from platform norms only when measured task gains clearly repay the learning tax.
- **Density vs simplicity**: Calibrate to surface mode — daily **operate** workspaces need high data density with low chrome noise (aligned tables over puffy cards), whereas **onboard/persuade** screens need chunked focus (<=4 ungrouped options) and progressive disclosure capped at two layers.
- **Undo vs confirmation**: Verify the backend actually supports reversal (soft delete, deferred commit, compensating action) before promising undo; reserve blocking, consequence-named confirmation for mutations both severe and irreversible.
- **Optimistic vs pessimistic updates**: Use optimistic UI on high-probability, low-risk, reversible actions with explicit failure rollback; await server confirmation when money, permissions, uniqueness, or external side effects are on the line.
- **Honest defaults**: Preselect the user's most common legitimate intent; reject deceptive dark patterns and surface the conflict if asked to build one.

Keep observed user behavior distinct from heuristic predictions, ranking issues by **frequency, impact, and persistence** ([references/evaluation.md](references/evaluation.md)).

## Engineer complete state machines, including unknown outcomes

Every control and view is a state machine, not a happy-path screenshot:

- **Controls**: handle `default`, `hover`, `focus-visible`, `pressed`, `disabled` (stating how to enable when user-resolvable, or hiding when permission-gated), `pending` (size-stable, double-submit locked), `success`, and `error`.
- **Views**: handle `first-use`, `empty` (with a direct starting action), `loading`, `partial`, `full`, `slow`, `offline`, `permission-denied`, and `partial-failure` while keeping unaffected regions usable.
- **Timeouts and dropped connections are unknown outcomes, not definite failures**: the write may already have committed. State whether local input is safe, reconcile server state before offering retry, and allow immediate retry only when API idempotency is verified.
- **State preservation**: retain drafts, filter/sort URL state, selection, and scroll across errors, reloads, and Back navigation — clearing only secrets and one-time codes.

Keep hover, touch gestures, and color strictly supplementary: pair every capability with keyboard-operable semantic markup, logical focus order, polite vs assertive live announcements, non-drag pointer alternatives, and comfortable target sizes. Load [references/interaction-patterns.md](references/interaction-patterns.md) for component mechanics, [references/content-and-localization.md](references/content-and-localization.md) for microcopy and i18n, [references/cli.md](references/cli.md) for CLIs, and [references/ai-interaction.md](references/ai-interaction.md) for AI/agent UX or AI-generated UI constraints.

## Dogfood live flows across function, density, and AI slop

Never sign off on JSX inspection or a static screenshot alone. Whenever a running build is reachable, **dogfood the live product end-to-end** as both a cold first-time user and a 10x/day repeat operator — preferring `ego-lite` (`ego-browser`, running `ego-browser skill` first) on web UIs for real rendering and shared-session fidelity, falling back cleanly to available browser automation if `ego-lite` is absent, and exercising interactive TTY plus piped non-TTY runs on CLIs:

- Run a cold **5-second eye-order & 2-second region scan** before clicking: verify visual hierarchy matches the primary job and cut or merge regions, hollow widgets, or stacked features that fail to earn their keep.
- Stress complete loops with realistic messy inputs across keyboard-only navigation, empty/slow/definite-error/unknown-timeout paths, reload survival, destructive undo/confirm gates, and local AI output repair.
- Audit **information density** (fixing starvation density on operator views and overload/chrome noise on onboarding) and strip **AI slop** (unmotivated purple gradients, symmetrical 3-column icon-circle grids, nested card-in-card chrome, happy-talk banners, and vague `Submit`/`Get Started` copy).

Use [templates/INTERACTION-SPEC.md](templates/INTERACTION-SPEC.md) for specifications and [templates/INTERACTION-REVIEW.md](templates/INTERACTION-REVIEW.md) for reviews.

## Done when

Scoped to touched flows: **Design** delivers anti-bloat object structure, complete state machines (including unknown outcomes), backend-honored undo/confirm policies, novice-to-expert paths, accessibility semantics, and explicit principle trade-offs. **Review** ranks concrete findings by `frequency x impact x persistence`, labels `observed | measured | predicted` evidence, calls out feature bloat, density mismatches, and AI slop directly, and gives convention-aligned fixes or cuts. **Implementation** proves all specified states, keyboard paths, density/craft bar, and data-preserving recovery in live dogfooding (`ego-lite` preferred on web), reporting any unexercised state explicitly.
