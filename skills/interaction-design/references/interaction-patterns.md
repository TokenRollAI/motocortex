# Interaction Patterns

Each pattern below exists to close the loop between an action, the system's response, and the next step. Adapt them to the platform's native components and the product's design system; the reasoning matters more than the exact form.

## Controls and asynchronous actions

Give interactive surfaces consistent hover, focus-visible, and pressed states from one shared definition, so every control signals operability the same way. Hover only enhances; the control must be discoverable and usable without it.

An asynchronous button moves through pressed, pending, and then success, failure, or unknown outcome. While pending, keep its size stable, block duplicate submission, and show progress locally rather than covering the page. On success, confirm in place and offer undo when the change is reversible. On a definite failure, keep the user's input and state how to retry.

A timeout or dropped connection is not a definite failure: the server may already have sent the message or charged the card. Treat it as an unknown outcome. Say so plainly, keep the input, and resolve the outcome by querying or reconciling state before offering a retry. Offer an immediate retry only when the existing API makes it safe, for example through an idempotency key or a natural deduplication rule; verify that support in the code or API contract rather than assuming it.

Model feedback per action rather than per mockup. A shape such as the following keeps the whole lifecycle in one place:

```ts
type AsyncState = "idle" | "pending" | "success" | "failure" | "unknown";

interface ActionFeedback {
  state: AsyncState;
  message?: string;
  recoverAction?: "retry" | "undo" | "cancel" | "check-status";
}
```

## Save and sync status

Show saving status in text next to the content it concerns: saving, saved, or failed. A failure message must say whether the work is still safe locally and what will happen next, for example that it will retry after reconnecting. Announce these changes through a polite status region so assistive technology reports them without stealing focus.

## Loading

Choose the indicator from what the system knows. When the structure of the result is known, show a skeleton of that structure. When progress is measurable, show determinate progress. For short, uncertain waits, a small spinner near the pending region is enough. For long work, run it in the background with visible status and a way to cancel. Avoid full-page loading for a local action, since it discards context and makes small actions feel expensive.

## Forms and errors

Validate at the point where a correction is cheap, show errors next to the field that caused them, and associate the message with the field programmatically. After a failed submission, also summarize the errors and move focus to the summary or the first invalid field. Pair error color with text or an icon. Keep entered values after any failure, except secrets and expiring credentials, which are cleared by convention.

## Destructive and irreversible actions

For reversible deletion or overwrite, act immediately and offer undo, a trash, or version history. For irreversible, high-impact actions, show the affected objects and consequences first, then require an explicit confirmation whose button names the action, such as "Delete 3 projects" rather than "OK". Avoid confirmation on routine actions; frequent dialogs train people to dismiss them unread.

## Tooltips, toasts, and snackbars

Tooltips explain; they do not contain essential functions or information. Show them on both hover and keyboard focus, keep them dismissible, and associate them with their trigger as a description.

Toasts and snackbars suit brief, non-blocking confirmations, and a snackbar is a good place for an undo action. Give actionable messages enough time to be used, and never rely on a disappearing toast as the only channel for an error the user must resolve.

## Empty states and onboarding

An empty state explains what belongs here, why it is useful, and offers one clear next step, such as creating an item, importing data, or starting from a template or example. "No data" alone leaves the user stuck.

Let people complete the first task directly. Introduce a feature with a contextual hint when it first becomes relevant, and keep hints skippable and dismissible. A long, mandatory product tour asks people to memorize features before they have any context for them.

## Accelerators

Show shortcuts in menus, tooltips, and the command palette, next to the visible action they speed up. A command palette should search commands by name and synonyms, show their shortcuts, and act on the current selection or context. Bulk actions and saved views should preserve the same undo and confirmation policies as single actions.

## Drag and drop

Highlight valid drop targets only while dragging over them, and give invalid targets a clear refusal signal. Show where the item will land before release. Provide two separate paths beyond dragging. First, a single-pointer path that works by clicking or tapping, such as a move menu, move-up and move-down buttons, or tap-to-select then tap-destination, for people who cannot perform precise drags; WCAG 2.2 success criterion 2.5.7 requires this, and keyboard support alone does not satisfy it. Second, keyboard operability of the same outcome for keyboard and switch users, as a distinct requirement.

## Data tables and lists

Lead each row with a human-readable identifier rather than a generated ID, and order columns by importance to the task. Keep headers, and usually the first column, visible while scrolling. Make filtering easy to find, fast, and clearly indicated when active, including a count of what the filter hides and a one-step way to clear it. Apply filters instantly when results return within about a second; when they may be slower, let people apply a batch of filter changes at once.

Support bulk selection with checkboxes and a select-all that states its scope, such as the current page or all matching results. Let people hide and reorder columns without relying on dragging, and indicate when columns are hidden. Prefer a non-modal side panel for editing a row, since people often need to refer to other rows while they edit.

Use pagination or a "load more" control when people look for specific items, compare, or need to reach content below the list; reserve infinite scroll for homogeneous feeds meant for browsing. Whatever the choice, restore the position, filters, and sort when people return. Keeping view state in the URL is a common way to make it shareable, restorable, and consistent with the back button.

Use a native table for static tabular data. Use an interactive grid pattern only when cells are editable or individually actionable; it takes a single tab stop and moves between cells with arrow keys, which becomes hard to use when the cells contain controls that also need arrow keys.

## Search

Search the broadest sensible scope by default, show the scope that was searched, and let people narrow results afterwards with filters rather than choosing a scope before searching. Make suggestions visually distinct from the typed text, highlight the matching words, and always allow searching exactly what was typed; avoid preselecting a suggestion when suggestions can arrive late, since the enter key would then search something the person did not type.

A zero-result page must say clearly that nothing matched, show what was searched, and offer a way forward, such as spelling corrections, broader scope, removing filters, or related content. Many people abandon after one failed search instead of rephrasing, so the recovery must be on the page. When correcting a query automatically, say so and offer the original.

## Notifications

Classify each notification by honest urgency, and let only time-critical events interrupt; route the rest to passive channels such as an inbox, badges, or scheduled digests. Give each kind of notification its own channel or category so people can control them independently, and respect platform focus and do-not-disturb modes. Ask for notification permission after showing the value, explain what will be sent, and keep promotional messages separate, opt-in, and never labeled as urgent.

Make every notification actionable and self-contained, with a direct path to the relevant object and enough context to resume work there. Clear badges and indicators once the person has seen what they point to. Do not rely on a badge or a transient notification as the only channel for something that requires action.

## Collaboration and concurrency

Show who else is present, what they are viewing or editing, and who can see a shared object. Make sharing and permission state visible where people decide what to write, not only in a settings page. When one person follows or highlights another's view, make it visible to both and easy to decline.

Choose a conflict strategy that fits the data. Property-level last-writer-wins, where the server orders changes, is simple and works when concurrent edits to the same property are rare and cheap to redo; text and structured documents usually need merging; exclusive locks suit cases where merging is meaningless or costly, as long as the lock holder, its age, and a way to take over are visible. When a conflict cannot be resolved automatically, show both values and let a person choose rather than silently discarding work, and keep a readable version history so any outcome can be inspected and restored.

For offline or local-first work, show clearly what is saved locally, what has synchronized, and what is waiting, and surface conflicts after reconnecting at the objects they affect.

## Mobile and touch

Hidden gestures are rarely discovered and easily forgotten, even after a hint. Offer a visible control for every gesture-driven action, reserve swipe actions on list items for conventional operations such as delete or archive, and keep swipe meanings consistent across the app. Prefer system gestures to custom ones, and do not override system back navigation to run logic unrelated to the visible UI state.

Size touch targets for fingers, around 44 by 44 points on iOS and comparable density-independent sizes elsewhere, with spacing around them. Touch accuracy drops toward screen edges and corners, so give edge targets extra size and keep destructive controls away from frequently used ones. People switch grips often, so avoid designs that only work for one hand position. Keep content and controls inside the platform's safe areas.

## Motion

Use motion to show where something came from or went, that state changed, or where attention should move. Keep it short enough not to delay information, and remove or reduce it under reduced-motion preferences.

