---
name: product-dogfood
description: >-
  Operate a live product end-to-end like a real user and deliver candid,
  evidence-backed critique across functional design, interaction, UI craft,
  information density, and AI slop. Use when asked to dogfood, try out, walk
  through, experience deeply, or audit a running web app, desktop surface, CLI,
  or workflow from a product and user perspective to expose what feels broken,
  hollow, tedious, sparse, noisy, or templated. Do not use for pre-build
  interaction specs, implementing UI edits without live product usage, static
  code or architecture review, or automated test-suite authoring.
---

Code inspection and static screenshots hide what a product actually feels like to learn, operate at speed, and trust. Dogfooding means driving the running product cold with real user goals, feeling every broken loop, extra click, misweighted viewport, and unedited generator tell firsthand, then turning that evidence into blunt, prioritized product cuts and fixes.

## Walk the live product blind before touching source

Reading routes, schemas, or components beforehand plants an insider's mental model and masks confusing onboarding, leaky internal naming, and missing signifiers. Enter the live product cold first. Within the first five seconds on the entry and main workspace views, capture your unfiltered read: what the product claims to do, the first three elements that pull the eye, and whether the path to first value is obvious without outside context.

Inspect repository code, network payloads, or configuration only **after** finishing the live walkthrough, and only to distinguish an unbuilt capability from a broken implementation, confirm a root cause, or inspect a state blocked in the live environment. Keep live user observations strictly separated from post-walkthrough source checks.

Leave product code, shared data, and shared browser profiles intact: use reversible or clearly scoped synthetic records during write flows, and never edit source code, mutate shared production state destructively, or clear shared browser cookies/storage without explicit user authorization.

## Prefer ego-lite on web surfaces, falling back cleanly

A shared real browser preserves true font rendering, viewport density, signed-in session state, and live human handoffs that isolated test runners miss. On web targets, **prefer `ego-lite` (`ego-browser`) first** whenever available — run `ego-browser skill` before the first browser call, reuse one `TaskSpace`, protect shared cookies and user tabs, and use `handOff()` when unprovided credentials, SSO, 2FA, CAPTCHA, payment, or browser permission prompts require the user.

When `ego-lite` is absent or unavailable in the current environment, fall back pragmatically to the strongest available live browser tool (such as `agent-browser`, a browser MCP server, or Playwright/Chromium automation) rather than stalling — recording which driver ran and any session or rendering caveats (such as a clean unauthenticated profile). Report a browser blocker only when *no* live browser runtime can reach the target, never fabricating visual or interactive claims from JSX/CSS alone. Read [references/web-exploration.md](references/web-exploration.md) when operating web targets. On CLI or API surfaces, execute the real binary or endpoints across interactive TTY, piped non-TTY, and error paths.

## Stress full value loops from cold start to operator speed

Clicking top-level nav tabs only proves routes mount. Exercise the product from two distinct postures: a **first-time user** trying to reach real payoff unassisted, and a **repeat operator** running the core loop ten times in a row where modal friction, focus resets, and missing shortcuts compound.

Carry realistic, messy domain inputs (long titles, multi-line text, edge characters, zero/large counts — never `test` or `foo`) through the full object lifecycle: create -> inspect -> edit -> search/filter -> export/share -> delete/undo. Deliberately probe empty states, zero-result searches, invalid submissions, slow/failing requests, mid-flow browser reloads and Back navigation, keyboard-only operation, and desktop vs mobile viewports where applicable. Reproduce interactive bugs once from a clean prior state to confirm them, logging findings and artifact paths incrementally as you go.

## Judge directly across the five product lenses

Zero console errors does not mean a good product. Evaluate every exercised journey across five lenses, calibrating severity with [references/critique-lenses.md](references/critique-lenses.md):

- **Functional design**: Does the feature set close the user's real job end-to-end, or stop at a demo happy path? Call out missing table-stakes links, dead-end outputs, backend-shaped navigation, and hollow features or panels that should be cut or demoted.
- **Interaction and flow**: Count clicks, modal hops, scroll jumps, and memory bridges across screens. Audit async state lifecycles, draft/filter survival across reloads, undo vs named destructive confirmation, and keyboard/bulk speed on repeat workflows.
- **UI and visual craft**: Test whether visual weight matches task priority, and check cross-screen token coherence (type scale, spacing rhythm, radii, contrast, non-hover signifiers, responsive integrity).
- **Information density**: Judge density relative to surface mode — flag **starvation density** (puffy cards, hero banners, modal-hidden attributes, wasted above-the-fold space) on daily operator views, and **overload density** (unchunked option walls, premature advanced flags, chrome noise) on onboarding or infrequent decision views.
- **AI slop**: Apply the studio test — would a deliberate product team choose this styling, structure, and copy for *this* domain? Call out unmotivated generator tells across visuals, layout templates, and vaporware/happy-talk microcopy, distinguishing brand-owned choices from stacked defaults.

## Deliver candid, ranked fixes backed by runtime proof

Skip diplomatic fluff and vague taste notes ("clean up layout", "improve UX"). State plainly what earns its keep, what hurts comprehension, speed, or trust, and what to **cut, merge, redesign, or rewrite**.

Order findings `P0` -> `P3` by user and product impact. Anchor each finding in the user job, exact route/command, captured runtime proof (screenshots, snapshots, DOM/network/console signals), causal harm, and a concrete replacement — down to the exact flow restructure, table/layout change, feature cut, or rewritten label. Use [templates/DOGFOOD-REPORT.md](templates/DOGFOOD-REPORT.md) for full critiques, scaling tightly when scoped to a single flow.

## Done when

The live product has been driven end-to-end across core jobs and edge states (preferring `ego-lite` on web targets when available, or a documented live browser fallback otherwise, while leaving product code and shared profile data intact); feedback covers functional design, interaction, UI craft, information density, and AI slop with blunt, `P0`–`P3` ranked, actionable replacements; every claim cites captured runtime evidence cleanly separated from any post-walkthrough source check; and any blocked surface or role is stated explicitly alongside what unlocks it.
