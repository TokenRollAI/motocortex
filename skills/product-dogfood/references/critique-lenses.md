# Product Critique Lenses

Use these five lenses while operating the product so feedback covers whether the product is worth using, not merely whether its buttons throw exceptions. Weigh findings by how often real users hit them, how badly they stall or degrade the outcome, and whether users can recover.

## First-impression and region scan

Run a five-second read on the landing screen and the primary workspace before clicking anything. Record what the screen communicates at a glance, the first three elements the eye lands on in order, and whether those three match the user's real reason for arriving. When a secondary badge, decorative banner, or sidebar promo beats the primary action for attention, the visual hierarchy is lying.

Apply a two-second region scan to each major view: name the job of every distinct area on screen. Regions whose job takes longer than two seconds to name, or two regions doing the same job in slightly different shapes, signal muddled structure that should be merged or cut.

## Functional design

Functional critique asks whether the product solves the whole problem it promises rather than staging a narrow demo.

Trace the core domain object from creation to real-world payoff. An editor without export or sharing, a search bar without useful filters or sort on growing lists, an import without validation feedback, a background job without status or cancellation, or a generated artifact trapped in a read-only pane leaves the workflow half-built. Name the exact missing link that blocks real adoption.

Apply the earn-your-keep test to every tab, dashboard widget, and setting. Early products routinely accumulate speculative analytics panels, redundant views, social chrome, or configuration toggles copied from larger tools while the primary workflow stays rough. Recommend removing or demoting features that add navigation weight without serving the main user job; subtraction is often the sharpest product improvement.

Check whether objects and navigation match user concepts. People think in projects, invoices, deployments, or drafts, not join tables, internal microservices, or pipeline stages. When a single user goal forces jumping across three top-level sections to assemble context, call out the broken boundary and propose co-locating the workflow.

## Interaction and flow

Interaction critique measures the physical and mental tax of completing and repeating work.

Count steps, clicks, scroll jumps, and focus resets along both first-time setup and the ten-times-a-day operator loop. Flag modal overuse where inline editing, a side panel, or direct manipulation preserves context better. Flag memory bridges where step three asks for information visible only back on step one, and modes that force clicking "Edit" and "Save" around trivial single-field adjustments.

Exercise the full state lifecycle of asynchronous and stateful views: empty state on a new account, zero-result filter state, loading skeletons or pending indicators, partial or full request failure, ambiguous timeout, and browser reload or back-navigation mid-task. Verify that drafts, filter selections, and scroll positions survive navigation and recoverable errors, and that errors sit beside their cause with a concrete way forward rather than flashing in a disappearing toast.

Match safeguards to blast radius and reversibility. Routine reversible actions should happen immediately with undo or history; high-stakes, irreversible actions (deleting shared resources, billing, sending externally, revoking access) should state the concrete consequence and name the verb on the confirmation trigger rather than training users to click past generic "Are you sure?" dialogs. Check keyboard reachability, focus visibility, and expert shortcuts on high-frequency surfaces.

## UI and visual craft

Visual craft serves comprehension, trust, and scanning speed.

Establish whether each view has one unmistakable focal point, grouped secondary controls, and quiet supporting chrome. When every card border, shadow, pill badge, and heading carries the same contrast, the eye has nowhere to start.

Compare the inferred design system across at least three screens — actual rendered typefaces, font sizes and weights, line heights, spacing increments, border radii, icon styles, button heights, and semantic status colors. Drift across screens makes a product feel stitched together by separate hands. Check that interactive controls carry consistent signifiers without relying on hover or color alone, prose stays readable (roughly 60 to 80 characters per line), interactive targets remain comfortably clickable or tappable, and layouts adapt across desktop and mobile widths without horizontal overflow or clipped labels.

## Information density

Information density is neither "less is better" nor "pack everything in"; judge it against the surface's job and user frequency.

On **operate surfaces** — workspaces, tables, queues, logs, editors, and admin consoles — people return daily to scan, compare, triage, and act. The dominant failure here is **starvation density**: marketing-sized hero headers inside a working app, puffy card grids showing four records where a compact table shows twenty-five, wide empty margins beside truncated titles, or hiding status and primary actions behind per-item menus and modals. Recommend tighter row rhythm, tabular alignment, scannable columns, and inline actions so operators see working context in one viewport without constant scrolling.

On **onboard and persuade surfaces** — first-run setup, landing pages, pricing, and rare high-consequence choices — people lack a mental map of the product. The dominant failure here is **overload density**: walls of ten ungrouped options at a single decision point (exceeding the roughly four chunks working memory holds comfortably), exposing advanced flags before basic setup works, or mixing primary setup steps with secondary upsells and documentation links. Recommend chunking, sensible defaults, and progressive disclosure limited to one clear next layer.

Separate **data density** from **chrome density**. High data density with shared headers, clean alignment, and restrained typography speeds experts up; high chrome density — boxes inside boxes, repeated field labels on every tile, redundant icons next to plain words, and status pills on every row when 98% share the same healthy state — creates clutter even when very little information is shown.

## AI slop

AI slop is the recognizable cluster of unchosen generator defaults across styling, page structure, and copy that strips a product of identity and makes users suspect nobody cared enough to design it. Judge by intent and craft rather than mechanical keyword bans: a single trait owned deliberately by a brand can work, whereas multiple unmotivated defaults stacked together expose template output.

Watch for **visual tells**: unmotivated purple, indigo, or blue-to-violet gradients; neon-accent-on-near-black developer clichés or warm-cream-plus-terracotta editorial defaults detached from the product's domain; gradient headline text and gradient primary buttons; frosted glass and radial background spotlights pasted across ordinary panels; uniform large border-radius and identical soft drop shadows wrapping cards inside cards in place of real layout; unstyled default system fonts with flat weight contrast; decorative blobs, wavy dividers, geometric filler illustrations, or emoji (`✨`, `🚀`, `⚡`) standing in for hierarchy and iconography.

Watch for **structural tells**: the symmetrical three-column feature grid (icon in a tinted circle, bold title, two-line blurb) applied regardless of what the content actually needs; tracked-out ALL-CAPS eyebrow chips above every section heading; `01 / 02 / 03` numbering on unordered concepts; bento grids giving equal box area to unequal ideas; placeholder or unverifiable social proof ("10,000+ happy teams", five-star quote strips without real attribution); decorative sparklines, progress rings, or fake dashboard widgets that represent no real user data; and routing every secondary action into a centered modal.

Watch for **copy and microcopy tells**: vaporware headlines ("Unlock the power of...", "Supercharge your workflow", "Your all-in-one intelligent platform"); happy-talk welcome paragraphs at the top of workspaces that repeat what the navigation already says (count how many words on a working screen can be cut without losing meaning); spaced em-dash slogans ("Built for speed — designed for scale") and middle-dot taglines ("Fast · Secure · Effortless"); vague button labels ("Get Started", "Learn More", "Submit", "Continue") instead of specific outcome verbs ("Create project", "Invite teammate"); apologetic or chatty error filler instead of plain cause-and-fix wording; and multi-sentence helper text compensating for a control whose label and structure should have been self-explanatory.

## Priority calibration

Rank findings so the team fixes product-defining problems before polishing corners:

- **P0 (Blocking)**: A core user journey cannot complete, user data or drafts are silently lost or corrupted, navigation or auth traps the user, or crashes and unhandled failures break primary workflows.
- **P1 (Major product or UX flaw)**: A table-stakes capability is missing from the core loop, a frequent operator workflow suffers heavy click or context-switch tax, severe starvation or overload density cripples scanning, or pervasive AI slop undermines trust on primary screens.
- **P2 (Moderate friction or craft gap)**: Secondary flows confuse or stall, empty/loading/error states are missing or unhelpful, component styles or vocabulary drift across pages, responsive layouts clip or overflow, or localized slop and vague copy weaken clarity.
- **P3 (Polish)**: Minor alignment, spacing rhythm, typographic hierarchy, edge-case truncation, or microcopy tightening.
