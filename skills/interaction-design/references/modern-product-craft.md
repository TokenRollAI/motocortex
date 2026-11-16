# Modern Product Craft: Subtraction, Classic Exemplars, and Live Dogfooding

Great modern software feels effortless not because it does less, but because it **refuses to stack every capability onto the primary viewport**. When a product grows by bolting a new tab, toolbar button, card, or settings toggle onto the screen for every new requirement, cognitive load compounds until both newcomers and daily operators drown in chrome.

## How benchmark products scale capability without stacking UI

Study the structural mechanisms behind modern category-defining interfaces — copy their underlying discipline, not their surface paint:

- **Linear — Opinionated defaults, monochrome calm, and command-indexed power**: Linear rejects blank-slate enterprise configuration sprawl in favor of one sharp default workflow. Its workspace stays predominantly monochrome (using subtle lightness/opacity steps for elevation) so saturated color carries instant semantic weight (status, priority, blockers) rather than decorative noise. Instead of crowding every issue row with fifteen action buttons, the primary list stays dense and scannable while every secondary mutation (`Assign`, `Move to cycle`, `Link PR`, `Change status`) lives one keystroke away in a contextual `Cmd+K` command menu or hover/selection shortcut. *Takeaway: index power into searchable, selection-aware commands rather than paving the viewport with buttons and settings.*
- **Google Search, Drive, and Gmail — Single-intent entry, progressive enabling, and Undo over nagging**: Google Search puts an entire retrieval engine behind one unmistakable input, disclosing facets and filters only *after* user intent is expressed. Google Drive keeps row chrome quiet until items are selected, surfacing batch action bars contextually upon selection ("progressive enabling"). Gmail popularized executing routine side effects immediately with a crisp `Undo Send` window instead of training users to click blindly past "Are you sure?" modals. *Takeaway: show only what the current state justifies, and buy speed through reversibility rather than confirmation friction.*
- **Stripe and Figma — Flat primary surfaces with contextual lateral disclosure**: Stripe handles deep financial and API state while keeping primary tables summary-clean (amount, status, customer, timestamp); selecting a record opens a lateral drawer (or progressive accordion) for logs, risk signals, and refunds without destroying spatial list context. Figma packs desktop-grade authoring into a calm canvas by making the right-hand inspector strictly state-driven: typography controls appear only when text is selected, stroke/boolean tools only on vectors, and layout guides only on hover/selection. *Takeaway: let the active object summon its own controls instead of docking permanent multi-row toolbars.*

## Design by subtraction and earn-your-keep audits

Before adding any panel, tab, stat card, modal, or preference toggle, force it through three gates:

1. **Does it close the primary user loop, or compensate for an unmade product decision?** Adding a "Configure view" toggle because the team could not decide on a good default exports design laziness onto every user. Pick the strong default; expose configuration only when distinct personas genuinely have incompatible workflows.
2. **Can an existing object or command absorb it?** Prefer an inline state on the domain object, a contextual drawer section, or a command-palette verb over a new top-level navigation item.
3. **What leaves the screen to pay for it?** Treat viewport attention as a fixed budget. On reviews and redesigns, explicitly recommend **cutting or demoting** decorative dashboard widgets, redundant summary cards, and low-frequency controls that dilute the primary action.

## Calibrate information density and strip AI slop

Pair interaction state design with direct visual, density, and anti-slop discipline:

- **5-second eye-order & 2-second region scan**: On cold entry, verify that the first three elements capturing the eye match the user's primary job, and that every distinct screen region can have its single job named within two seconds; merge or delete regions that fail.
- **Mode-matched density (data density vs chrome density)**: Daily **operate** views (tables, queues, workspaces, consoles) fail through *starvation density* — oversized hero headers, airy 4-card grids where a compact aligned table fits 25 rows, or attributes hidden inside per-row modals. **Onboard and persuade** views fail through *overload density* — walls of 8+ ungrouped choices exceeding ~4 working-memory chunks, or premature advanced flags. Always cut *chrome density* (nested card-in-card borders, repeated field labels, redundant icons, uniform "Active" pills on 99% healthy rows) before hiding real data.
- **Zero-tolerance for AI slop**: Reject unchosen generator defaults that make interfaces look stamped out and untrustworthy — unmotivated purple/indigo gradients, symmetrical 3-column icon-in-circle feature grids, uniform bubbly cards nested inside cards, radial background glows everywhere, ALL-CAPS eyebrow chips above every heading, emoji section headers, vaporware/happy-talk welcome banners inside working screens, and vague `Get Started` / `Submit` CTAs instead of specific outcome verbs.
