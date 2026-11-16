---
name: product-dogfood
description: >-
  Use a live product end-to-end as a real user and deliver candid,
  evidence-backed feedback across functional design, interaction, UI craft,
  information density, and AI slop. Use when asked to dogfood, try out, walk
  through, experience deeply, or critique a running web app, desktop surface,
  CLI, or product workflow from a user and product perspective, or to expose
  what feels broken, hollow, tedious, sparse, noisy, or templated. Do not use
  for designing an interaction spec before a product runs, implementing UI
  changes without live product usage, static code or architecture review, or
  writing automated test suites.
---

Reading source code or glancing at static screenshots hides how a product actually feels to learn, operate, and trust. Deep dogfooding means using the running product with a real user's goals and ignorance, experiencing every dead end, missing capability, extra click, misweighted viewport, and unedited generator cliché firsthand, then turning that lived friction into direct, prioritized product recommendations.

## Experience the product blind before reading source

Inspecting routes, components, schemas, or prompts beforehand gives you an insider's mental model and masks confusing onboarding, ambiguous labels, and missing signifiers. Enter the running product as an outsider first. Within the first seconds on the landing or workspace view, record your unfiltered impression: what the product appears to do, which three elements pull the eye first, and whether the path to first value is obvious without outside explanation.

Read repository source, network payloads, or configuration only after completing the live walkthrough, and only when needed to separate a broken implementation from an unbuilt capability, verify a root cause, or inspect a state the live environment could not reach. Keep live observations clearly distinct from post-walkthrough source checks so insider knowledge never rewrites what a user actually saw.

Leave the target repository and shared environment intact. A dogfooding request authorizes realistic usage with reversible or clearly scoped test data, whereas editing product code, mutating shared production data destructively, or wiping shared browser profile state requires explicit user direction.

## Drive web surfaces with ego-lite, not synthetic test runners

A real shared browser exposes actual font rendering, viewport rhythm, authenticated workflows, and human handoffs that headless test scripts flatten away. On web targets, drive the live product exclusively through `ego-lite` (`ego-browser`), running `ego-browser skill` first so scripts follow the installed runtime contract. Use semantic snapshots to orient and act, viewport and full-page screenshots to judge visual hierarchy and density, and in-page evaluation or CDP when console errors, network failures, or computed style metrics inform the critique. Read [references/ego-lite-exploration.md](references/ego-lite-exploration.md) when operating a web target.

Keep Playwright, Puppeteer, and headless browser scripts out of web verification; if `ego-lite` or the target URL cannot run, report the specific blocker rather than substituting another browser harness or guessing runtime behavior from code. When login without supplied credentials, 2FA, CAPTCHA, payment, or a browser permission prompt requires a person, hand control to the user in the active space and resume there once they finish. Preserve existing cookies, storage, and user-owned tabs unless the user explicitly asks to clear state. For CLI or API products, execute the real commands across interactive, piped, and failure cases.

## Walk real jobs from first contact to repeat speed

Clicking through top-level navigation only checks that routes render. Real product weaknesses appear when carrying realistic, messy domain data across steps, recovering from mistakes, and repeating a task ten times in a row.

Adopt at least two angles while using the product: a first-time user trying to reach meaningful value unassisted, and a daily operator repeating the core workflow where extra clicks, modal jumps, and lost context compound. Carry core objects through their whole lifecycle — create, view, edit, search or filter, share or export, and delete or undo. Deliberately exercise empty states, zero-result searches, long or awkward strings, invalid inputs, slow or failed requests, mid-flow reloads, keyboard-only operation, and relevant desktop and mobile viewports. Confirm interactive bugs by reproducing them once, and record findings with screenshot or output paths as you go so nothing blurs across a long session.

## Critique directly across the five product lenses

A product that throws zero runtime errors can still fail if its features stop short of the user's job, its flows tax routine work, its hierarchy lies, its screens starve or drown the eye, or its interface looks stamped out by a template generator. Judge every exercised workflow across all five lenses, using [references/critique-lenses.md](references/critique-lenses.md) to calibrate severity and context:

- **Functional design**: Test whether capabilities close the real job from intent to usable outcome. Call out missing table-stakes steps, dead-end outputs that cannot be edited or carried forward, hollow features that add surface area without earning their keep, and navigation organized around backend tables instead of user objects.
- **Interaction and flow**: Measure the physical and cognitive tax of each task. Flag unnecessary steps, modal chains where inline action belongs, lost drafts or filters across navigation, silent waits, missing keyboard or bulk accelerators on repeat paths, and destructive actions that either omit undo or nag on routine edits.
- **UI and visual craft**: Check whether visual prominence matches task importance. Evaluate alignment, spacing rhythm, typographic hierarchy, color contrast, interactive signifiers without hover, state consistency across views, and responsive layout integrity.
- **Information density**: Judge density against the screen's job rather than equating whitespace with clarity. On operational workspaces, flag starvation density — oversized cards, decorative banners, or hidden row details that force constant scrolling and clicking to inspect a few items. On onboarding or infrequent decision views, flag overload density — unchunked walls of options, competing badges, and internal fields exposed before they matter.
- **AI slop**: Ask whether a thoughtful human team would deliberately choose this layout, ornament, and copy for this specific product. Flag templated visual tells (unmotivated purple-indigo gradients, symmetrical three-column icon-circle grids, uniform rounded cards nested inside cards, decorative blobs or radial glows, emoji headings), structural filler (ALL-CAPS eyebrow chips above every heading, invented stat strips, decorative sparklines, equal bento boxes for unequal content), and copy slop ("Unlock the power of...", welcome happy-talk inside workspaces, vague "Get Started" or "Submit" buttons, apologetic or robotic phrasing in place of plain task verbs). Weigh context honestly: a brand-owned trait backed by real craft differs from stacked generator defaults.

## Deliver candid, ranked recommendations

Polite padding and vague aesthetic notes ("simplify this section", "add polish") hide what matters and leave builders guessing what to change. State plainly what earns its place, what hurts the product, and what should be cut, merged, redesigned, or rewritten.

Rank findings from core-value blockers and high-frequency workflow taxes down to craft and microcopy polish. Tie each finding to the user goal, the exact route or command, captured evidence (screenshots, snapshots, console or network signals), the mechanism of user harm, and a concrete fix — naming the specific flow change, layout shift, capability cut or addition, or replacement copy. Distinguish live-observed facts from post-walkthrough source verification and from unexercised paths. Use [templates/DOGFOOD-REPORT.md](templates/DOGFOOD-REPORT.md) when writing a full product critique, adapting its depth when the user scopes to a single flow.

## Done when

The running product has been used end-to-end across its core workflows and relevant edge states — through `ego-lite` on web surfaces without Playwright or unrequested profile-state clearing — while leaving product code and shared data intact. Feedback covers functional design, interaction, UI craft, information density, and AI slop with candid, impact-ranked recommendations; every claim points to captured runtime evidence and separates live observation from any subsequent source check; and any flow, role, or environment that blocked live verification is explicitly named with what is required to exercise it.
