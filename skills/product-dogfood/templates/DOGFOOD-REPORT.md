# Product Dogfood Report Template

Write in the user's language with direct, unhedged product judgment. Strip placeholders, cite absolute or repo-relative paths to captured screenshots and runtime evidence, include only findings backed by real product operation, and rank `P0` -> `P3` by user and product impact.

<dogfood-report-template>
# [Product Name]: Product Dogfood Critique

[Target URL/CLI/version, date, viewports & surfaces exercised, signed-in roles/personas tested, and evidence directory]

## Blunt verdict

[Open with the cold 5-second read: what the product communicates at a glance, the first 3 elements the eye hits in order, and whether first value is immediately obvious. Follow with an unvarnished verdict on whether the product closes its core user job, what genuinely works, and the top 3 highest-leverage moves — explicitly including features or chrome to cut.]

## Journeys exercised

[Concise account of end-to-end tasks run cold (first-time user), at repeat speed (10x/day operator), and across edge/failure probes — noting step/click counts and exact points where momentum held or broke.]

## Critique by lens

### Functional design

[Loop closure from creation to payoff, missing table-stakes capabilities, hollow features/panels failing to earn their keep, and alignment between navigation/objects and user mental models.]

### Interaction and flow

[Click/modal/context-switch tax, memory bridges, state lifecycles (empty, pending, definite error, timeout, reload/Back preservation), undo vs named destructive safeguards, and keyboard/bulk speed.]

### UI and visual craft

[Focal hierarchy, contrast discipline, cross-screen token consistency (type, spacing, radii, status colors), non-hover signifiers, and desktop/mobile layout integrity.]

### Information density

[Signal-to-noise calibrated to surface mode (operator workspace vs onboarding/persuasion): above-the-fold data yield, starvation vs overload density, and chrome density vs real data density.]

### AI slop

[Visual, structural, and microcopy generator tells observed vs deliberate brand craft — paired with concrete structural, typographic, or copy replacements.]

## Prioritized findings

### [P0 | P1 | P2 | P3] [Crisp, direct problem statement]

- Lens: [`Functional` | `Interaction` | `UI craft` | `Density` | `AI slop`]
- Surface & task: [route, view, or command + user goal in flight]
- Evidence: [`live` | `live + source-verified`] — [screenshot path(s), repro steps, DOM metric, or console/network output]
- Impact: [exact behavior observed and how it blocks value, taxes speed, or erodes trust]
- Fix: [specific feature cut/addition, flow restructure, layout/density change, or replacement copy]

## Unverified surfaces and product forks

[Flows, permissions, integrations, or platforms blocked from live execution and what unlocks them, plus strategic product trade-offs reserved for the owner.]
</dogfood-report-template>
