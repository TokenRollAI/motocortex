# Product Dogfood Report Template

Use this skeleton when delivering a written product dogfooding critique. Write the report in the user's language with direct, unhedged judgment. Replace placeholders with concrete findings, embed or link captured screenshots and runtime artifacts by path, keep only findings backed by real usage evidence, and order findings by product and user impact.

<dogfood-report-template>
# [Product Name]: Product Dogfood Critique

[Target URL, CLI, or build version, date, viewports and surfaces exercised, signed-in roles or personas tested, and evidence directory]

## Blunt verdict

[Start with the unfiltered 5-second first impression: what the product communicates at a glance, the first three elements the eye lands on, and whether the path to first value is obvious. Follow with an honest summary of whether the product closes its core user job, what works genuinely well, and the 3 highest-leverage changes — including features or chrome to cut.]

## Journeys walked

[Briefly narrate the concrete end-to-end tasks attempted as a first-time user, as a repeat operator, and on edge or failure paths. Note step counts, time or click friction, and the exact points where momentum held or broke.]

## Critique by lens

### Functional design

[Assess whether features close the real user workflow end-to-end, which table-stakes capabilities are missing, which existing features or panels fail to earn their keep, and whether objects and navigation match the user's domain model.]

### Interaction and flow

[Assess click and context-switch tax, modal vs inline choices, state lifecycles (empty, loading, error, timeout, reload), undo and destructive safeguards, and keyboard or bulk efficiency for repeat use.]

### UI and visual craft

[Assess visual hierarchy, alignment and spacing rhythm, typographic scale, color and contrast discipline, interactive signifiers, cross-page consistency, and responsive behavior.]

### Information density

[Assess signal-to-noise ratio relative to the surface's mode (operational workspace vs onboarding or persuasion): call out starvation density, overload density, wasted viewport above the fold, or missing progressive disclosure.]

### AI slop

[Call out templated visual clichés, structural filler, decorative noise, and generic or happy-talk copy observed in the product, distinguishing unedited generator defaults from deliberate brand choices, and give concrete replacements.]

## Prioritized findings

### [P0 | P1 | P2 | P3] [Short, direct problem statement]

- Lens: [Functional design | Interaction | UI craft | Information density | AI slop]
- Surface and task: [URL, screen, or command, and the user goal in progress]
- Evidence: [observed live | observed live + source-verified], [screenshot paths, reproduction steps, or console/network output]
- What happens and why it hurts: [the concrete behavior and its cost to comprehension, speed, completion, or trust]
- Recommendation: [exact product, flow, layout, or copy change to make, and any trade-off]

## Unverified surfaces and open product choices

[Flows, permissions, devices, or external integrations that could not be exercised live and what is needed to test them, followed by product-direction trade-offs that belong to the owner.]
</dogfood-report-template>
