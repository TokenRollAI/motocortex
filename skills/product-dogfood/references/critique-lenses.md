# Product Critique Lenses

Apply these lenses during live operation so critique judges whether the product earns adoption and daily speed — not merely whether pages render without throwing.

## 5-second hierarchy and 2-second region scan

Before interacting on the landing screen or primary workspace, run two cold checks:

- **Eye-order check (5s)**: Name what the screen claims to do and the first three elements that capture attention in order. When a promo banner, secondary badge, or decorative header beats the primary user action, visual hierarchy is lying.
- **Region-job check (2s per block)**: Name the single job of every distinct region on screen. Any region whose purpose takes >2s to name — or two regions splitting the same job — is structural clutter to merge or cut.

## 1. Functional design

Judge whether capabilities close the real job-to-be-done rather than staging a demo:

- **End-to-end loop closure**: Follow the primary domain artifact from creation to downstream payoff. Generation without editing/export, lists without working filter/sort at realistic volume, imports without row-level error feedback, or background jobs without progress/cancel leave the product half-built.
- **Subtraction and earn-your-keep**: Challenge dashboards, tabs, decorative stats, and settings copied from category templates that do not serve the core loop. Recommending what to **delete or demote** is often higher-leverage than proposing new features.
- **User-object alignment**: Flag navigation or workflows organized around internal services, database join tables, or pipeline stages that force users to hop across multiple top-level views to finish one domain task.

## 2. Interaction and flow

Measure the physical and cognitive tax of cold setup and 10x/day operator repetition:

- **Action and context-switch tax**: Count clicks, modal-on-modal chains, separate Edit/Save ceremony on trivial fields, and *memory bridges* where step 3 requires recalling data visible only back on step 1.
- **State lifecycle and persistence**: Probe new-account empty state, zero-result search, pending/skeleton stability, definite failure, ambiguous timeout, mid-task reload, and Back button behavior. Check whether drafts, filters, selection, and scroll survive errors and navigation, and ensure actionable errors appear inline beside their cause rather than only in vanishing toasts.
- **Proportional safeguards and speed**: Routine reversible mutations should fire immediately with undo; irreversible high-blast-radius actions should name the exact consequence on the confirmation button. Check keyboard-only operability, `Enter`/`Escape` ergonomics, sensible defaults, and bulk/shortcut accelerators on repeat views.

## 3. UI and visual craft

Evaluate visual decisions by how fast and accurately they guide scanning and action:

- **Contrast budget**: One unmistakable primary focal point, quiet chrome, grouped secondary controls. Equal borders, shadows, and saturated pills everywhere flatten everything into noise.
- **Cross-screen token discipline**: Compare rendered font families, size/weight steps, spacing multiples, border radii, button heights, icon strokes, and status colors across 3+ screens to catch stitched-together drift.
- **Affordance and viewport integrity**: Interactive elements must signal operability without hover or color alone, prose should stay within readable measure (~60–80ch), targets must be comfortably clickable/tappable, and layouts must adapt across desktop and mobile widths without horizontal overflow or silent truncation.

## 4. Information density

Density fails in opposite directions depending on the surface's job:

- **Operate surfaces** (workspaces, queues, tables, logs, editors, consoles): Daily operators scan, compare, and triage. Watch for **starvation density** — oversized hero banners inside logged-in apps, airy card grids showing 4 items per viewport where a compact aligned table shows 25, truncated identifiers beside wide blank gutters, or hiding key attributes and actions inside per-row modals.
- **Onboard and persuade surfaces** (first-run setup, landing, pricing, rare high-stakes choices): Newcomers lack a mental map. Watch for **overload density** — walls of 8+ ungrouped choices at one decision point (exceeding ~4 working-memory chunks), exposing advanced flags before basic setup succeeds, or tangling primary setup with secondary promos.
- **Data density vs chrome density**: Separate useful information per viewport from box-inside-box borders, repeated labels on every card, redundant icons beside plain words, and uniform "Active" pills on 99% healthy rows. Cut chrome before hiding data.

## 5. AI slop

AI slop is the stacked residue of unchosen generator defaults across styling, page anatomy, and copy that makes a product look interchangeable and untrustworthy. Judge by intent and domain fit rather than keyword bans — one deliberate brand choice backed by craft differs from five unmotivated template defaults piled together:

- **Visual tells**: Unmotivated purple/indigo/blue-violet gradients; neon-on-near-black dev tropes or warm-cream + serif + terracotta editorial defaults unrelated to the subject; gradient text and gradient primary CTAs; frosted glass and radial background halos used everywhere instead of to show depth; uniform bubbly radii and identical soft shadows (`card-in-card-in-card`) replacing layout; unstyled `system-ui` stacks with flat hierarchy; decorative blobs, geometric filler art, or emoji headings/bullets (`✨`, `🚀`, `⚡`).
- **Structural tells**: Symmetrical 3-column icon-in-tinted-circle feature grids regardless of content shape; tracked-out ALL-CAPS eyebrow chips above every heading; `01 / 02 / 03` labels on non-sequential items; bento grids giving equal area to unequal concepts; unattributed social proof or invented stat strips (`10k+ users · 99.9%`); decorative sparklines/rings detached from real user data; routing every secondary action into a centered modal.
- **Copy tells**: Vaporware slogans (`Unlock the power of…`, `Supercharge your workflow`, `All-in-one seamless platform`); workspace happy-talk welcome paragraphs repeating what the sidebar already says (measure what fraction of screen words can be deleted with zero information loss); spaced em-dash aphorisms (`Built for speed — designed for scale`) and middle-dot chains (`Fast · Secure · Modern`); vague CTAs (`Get Started`, `Learn More`, `Submit`, `Continue`) instead of concrete outcome verbs (`Create workspace`, `Send invite`); chatty/apologetic errors; and multi-sentence helper prose compensating for an unclear control.

## Priority scale

- **P0 (Blocking)**: Core user loop cannot finish, user data/drafts silently vanish or corrupt, auth/routing traps the user, or crashes/5xx break primary paths.
- **P1 (Major product or UX flaw)**: Missing table-stakes capability on the core loop, heavy click/context-switch tax on frequent operator paths, severe density mismatch crippling scan/comprehension, or pervasive AI slop gutting credibility on primary views.
- **P2 (Moderate friction or craft gap)**: Confusing secondary flow, missing empty/loading/error/timeout state, cross-screen token/term drift, responsive breakage, or localized slop/vague copy.
- **P3 (Polish)**: Minor alignment, spacing, type scale, truncation, or microcopy tightening.
