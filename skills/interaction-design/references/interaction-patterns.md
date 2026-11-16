# Interaction Patterns

Component-level rules for closing the loop between user input, system state, and recovery. Adapt mechanics to the product's design system while preserving the behavioral invariants below.

## Async controls and unknown outcomes

Model async controls around five states rather than boolean `isLoading`: `idle | pending | success | failure | unknown`. While `pending`, lock dimensions, block duplicate submission, and scope indicators locally rather than masking the whole screen. On `success`, confirm in place and expose undo where supported. On definite `failure`, retain user input and place recovery next to the trigger.

Treat network drops and client timeouts as `unknown`: reconcile server state (or rely on a verified idempotency key / natural deduplication rule in the API) before offering retry so users never double-charge or double-send.

## Save status, loading, and forms

Display save/sync state inline beside the edited object (`Saving…`, `Saved`, `Offline — changes safe locally, retrying on reconnect`) via a polite live region that never steals focus. Match wait indicators to system knowledge: structural skeletons when layout is stable, determinate progress when measurable, compact local spinners for brief waits, and background execution with visible status + cancel for long jobs.

Validate forms when correction is cheap (on blur or submit, never mid-keystroke before valid input is finished), programmatically associate errors with fields, summarize failures on submit while moving focus to the first invalid control, and retain all non-secret inputs across errors.

## Destructive safeguards, toasts, and empty states

Use immediate execution + undo/trash/history for reversible edits. Reserve confirmation dialogs for irreversible, high-impact mutations, naming the specific affected objects and verb on the trigger (`Delete 3 projects`, never `OK` or `Yes`).

Keep tooltips strictly supplemental and reachable on both hover and keyboard focus. Reserve toasts/snackbars for non-blocking confirmations or undo affordances with generous timeouts — never as the sole channel for errors requiring user action. Turn empty states into starting points: state what lives here, why it matters, and provide the primary creation, import, or template action directly.

## Accelerators and drag-and-drop

Expose keyboard shortcuts beside menu actions and inside a searchable command palette, keeping bulk mutations under the same undo/confirm contract as single-item actions.

Every drag-and-drop interaction requires **two** independent non-drag paths: a single-pointer click/tap alternative (move menu, up/down controls, or select-then-place — required by WCAG 2.2 SC 2.5.7) **and** full keyboard operability, with valid/invalid drop feedback shown before release.

## Data tables, search, and URL state

Lead rows with human-meaningful identifiers, pin headers (and key identity columns on wide tables) during scroll, and show active filter counts with one-click reset. State explicit selection scope on bulk actions (`25 on this page` vs `all 412 matching`). Prefer non-modal side drawers for row editing so neighboring rows stay visible for comparison. Persist filter, sort, pagination, and drawer state in the URL so refresh, sharing, and Back work predictably; choose pagination or explicit load-more whenever users compare items or need footer access, reserving infinite scroll for casual feeds. Use native `<table>` semantics unless cells require spreadsheet-style arrow-key navigation (an ARIA `grid` captures arrow keys and clashes with embedded composite controls).

Search the broadest sensible scope first and narrow via post-search filters. Never auto-highlight late-arriving autocomplete items such that pressing `Enter` hijacks the literal typed query. On zero results, keep the query editable and offer concrete recovery (filter removal, broader scope, typo fallback with one-click revert to literal query).

## Notifications, collaboration, mobile, and motion

Route only genuinely time-critical events to interrupting channels; batch or inbox everything else, scoped by user-controllable category, with self-contained deep links that clear unread indicators on view.

Surface live presence, sharing scope, and permission bounds right where edits happen. Match concurrency resolution to data shape: property-level last-writer-wins for cheap independent fields, CRDT/OT merge for rich text, or visible expiring locks with takeover for unmergeable artifacts — surfacing unresolvable conflicts side-by-side with version history rather than silently overwriting work.

On touch devices, back every swipe or gesture with a visible control, respect platform back-navigation and safe areas, space destructive triggers away from frequent tap zones, and size targets generously (~44pt on touch, >=24px CSS minimum on pointer web). Use short motion only to clarify spatial origin, state transition, or focus shift, honoring `prefers-reduced-motion`.
