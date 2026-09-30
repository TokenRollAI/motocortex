---
name: interaction-design
description: >-
  Design, review, or implement user-facing interaction from user goals, mental
  models, evidence, and the full lifecycle of each action. Use when a task
  shapes how people discover, understand, perform, or recover from actions in a
  GUI, web or mobile app, dashboard, CLI, or AI/agent product: information
  architecture, navigation, forms, search and data tables, feedback and loading
  states, errors and undo, destructive or side-effecting actions, defaults,
  notifications, collaboration, interface copy, localization, onboarding,
  expert accelerators, accessibility, usability evaluation, or AI-generated UI.
  Do not use for purely visual styling, brand, or marketing work, for code
  changes that leave what users see, do, and recover from unchanged, or for
  routine edits that follow an existing pattern without adding states, risks,
  or flows.
---

Good interaction lowers the cost of understanding a system, predicting what an action will do, performing it, and recovering when it goes wrong. The aim is less cognitive work, not fewer pixels: people should guess less, remember less, wait less, and redo less, while state stays visible, actions stay findable, outcomes stay predictable, and mistakes stay recoverable. Visual styles come and go; these human constraints do not, so let them decide the design and let aesthetics serve them.

The hard part is rarely knowing the principles; it is choosing between them when they conflict and knowing whether a design works for the people who use it. Treat the guidance below as lenses for judgment, weighed against evidence about real users and tasks.

## Match the work to the task

Keep design, review, and implementation within the requested scope. A review can name a concrete failure scenario and the fix without rewriting the screen; a design must make flows, states, and recovery explicit enough to build; an implementation must also show that those states actually occur. Adding a field error to an existing form needs that field's error, recovery, and accessibility behavior, not a new information architecture. Pick the lenses the change actually touches.

Inspect existing product patterns, the design system, platform conventions, and the codebase's components before inventing anything. They are facts to reuse, and users have already learned them. Ask the user only about choices that change the product: who the primary user is, which risks are acceptable, and how to trade speed against safety.

## Start from people, tasks, and objects

State who uses this, how often, with what expertise, and what they are trying to get done. A first-time visitor, a daily operator, and an automation script need different entry points to the same capability. Identify the primary task, the secondary tasks, and the cost of getting each wrong.

Organize information around the objects and vocabulary users already recognize, such as projects, invoices, or pull requests, not around internal services, teams, or database tables. Every screen should answer where am I, what is here, and what can I do next. Keep navigation, lists, search, links, and URLs pointing at the same stable objects, so a person can arrive by any route and still know where they are.

Design order follows from this: user goal, then information architecture and principles, then interaction patterns, then components, then states and feedback. Starting from a good-looking page tends to hide missing states and misplaced objects until implementation.

## Ground decisions in evidence

A mental model is something to discover, not assume. Look first at what the product already knows: current usage and abandonment, support tickets and their wording, zero-result searches, and the conventions of the platform and neighboring products. Where the stakes justify it, watch a few representative users attempt the real task.

Keep predictions apart from observations. A heuristic finding is an expert's prediction that a design will cause trouble, and different evaluators routinely predict different problems; observed or measured behavior shows whether it does and how badly. Prefer task-level outcomes, such as success, time, errors, and abandonment, over opinions about the screen, and rank problems by frequency, impact, and persistence. [references/evaluation.md](references/evaluation.md) covers research methods, sample sizes, severity scales, and usability metrics; use it when planning a study, running a heuristic review, or deciding what to measure.

## Resolve tensions deliberately

When principles conflict, decide by the frequency of the action, the severity and reversibility of its consequences, the expertise of the people doing it, and the cost of learning something new. State the trade-off you chose so others can revisit it.

Consistency against innovation: people expect a product to work like the others they already know, so every departure from convention charges them a learning cost. Deviate only when evidence suggests the new pattern performs clearly better, or when the problem is genuinely different from the one the convention solves.

Density against simplicity: experts need information in view, and newcomers need a clear first step. Reduce the appearance of clutter through grouping, alignment, stable positions, and layering rather than by removing capabilities the target users need.

Disclosure against discoverability: put everything people use frequently in the first layer, choosing by observed frequency and importance rather than guesses. Make the path to the next layer obvious and well labeled, and avoid going beyond two levels of disclosure, where people tend to get lost.

Undo against confirmation: reversibility lets people act quickly and explore safely, while frequent confirmations train them to click through unread. Undo is not free, though; it requires soft deletion, deferred commits, versioning, or compensating actions, and it may not exist for effects that leave the system, such as sent messages or payments. Check what the backend can actually reverse before promising undo, and treat adding it as an architectural change when it is one. Reserve confirmation for consequences that are both serious and irreversible.

Optimistic against pessimistic updates: showing the result immediately makes common actions feel direct, and fits actions that usually succeed, are reversible, and are low risk, such as toggles, reactions, or edits without uniqueness constraints. Wait for confirmation when the action is irreversible, involves money or legal commitments, depends on server-side validation, or triggers external side effects. When an optimistic update fails, tell the person; a silent rollback looks like the system ignored them.

Defaults are decisions most people will never revisit. Choose the value that serves the most common legitimate need, make it visible and easy to change, and do not preselect options that benefit the business at the user's expense; a default seen as self-serving costs trust in every other default.

## Make state and action visible

People must be able to tell what the system is doing, whether their last action worked, and what they can do now. Show current status near the content it describes, and use interruptions such as modal alerts only for information that warrants breaking the user's context.

Prefer recognition over recall. Visible labels, menus, and suggestions beat commands the user must remember; an icon alone works only when its meaning is conventional for this audience. Give every interactive element a consistent signifier, such as shape, border, underline, cursor, or focus ring, that marks it as operable. Visual cleanliness that erases these cues trades a quieter screen for a harder one.

Hover may enrich an interface but must never be the only way to reach a function, since touch and keyboard users cannot hover. Gestures need a visible alternative for the same reason. Color may reinforce meaning but must be paired with text, an icon, or position, since some users cannot distinguish it. When an action is unavailable for a reason the person can resolve, say what would enable it rather than only disabling it; when the reason is permission or security, hiding the action may be the better choice.

## Treat every action as a state lifecycle

An interactive control is a small state machine, not a static picture. For each control, account for default, hover, focus, pressed, disabled, loading, success, and error where they apply; for each view, account for first use, empty, loading, partial, full, slow, offline, permission-denied, and partial-failure states. Missing states are the most common reason a designed screen feels broken in use.

Respect the classic response-time limits. Around 0.1 seconds feels instantaneous; around 1 second keeps the flow of thought intact though the delay is noticed; around 10 seconds is the limit of holding attention on the task. Acknowledge input within the first limit even when the result takes longer, match the waiting indicator to what the system knows about the wait, and keep the rest of the page usable while one region is pending.

When an asynchronous action fails, say what failed, whether the user's data is still safe, and what they can do next. A timeout is not a failure: the action may already have happened, so resolve the outcome before offering retry.

Preserve drafts, filters, selection, and scroll position across failures and navigation so a person never has to re-enter what the system already had. Secrets and expiring credentials, such as passwords, card security codes, and one-time codes, are the exception: clear them by convention and return focus to the field.

[references/interaction-patterns.md](references/interaction-patterns.md) covers concrete patterns for controls, save status, loading, forms, destructive actions, toasts, empty states, onboarding, accelerators, drag and drop, data tables and search, notifications, collaboration, mobile, and motion. Read the parts that match the components in scope.

## Prevent errors, then make recovery cheap

The best error is one that cannot happen. Constrain inputs to valid values, prefill what is known, make repeated submissions idempotent, and show the objects an action will affect before it runs.

Execute ordinary reversible actions immediately and offer undo, a trash, or version history. Scale safeguards to impact and frequency rather than to the type of action: sending a chat message calls for, at most, a short recall window, while sending a contract, paying, permanently deleting shared data, or granting broad access calls for naming the specific consequence before the action runs. For changes whose effect is hard to predict, show a preview or diff before applying.

Place error messages next to their cause, state what happened and how to fix it in plain language, and summarize errors when a submission fails. A disappearing toast alone is not an adequate channel for an error the user must act on.

## Write the interface

Words are interaction. Label actions with specific verbs that describe their result, use one term for one concept everywhere, put the most important words first so scanning works, and write for the user's task rather than the system's internals. Keep text flexible enough to survive translation, and never assemble sentences from fragments. [references/content-and-localization.md](references/content-and-localization.md) covers microcopy, error and confirmation wording, and localization constraints; read it when writing or reviewing interface text or building for more than one locale.

## Organize complexity for novices and experts

Keep the primary path short and always visible. Serve novices with visible paths and experts with accelerators: keyboard shortcuts, a command palette, bulk actions, saved views, and automation or API access. Teach the accelerator from the visible path, for example by showing the shortcut next to the menu item, so skill grows without sacrificing discoverability. Most people do not become experts on their own, so the visible path must remain complete rather than a teaser for hidden power.

Command-line tools follow the same principles through different channels: clear status commands, predictable verbs, helpful errors, human-readable defaults, stable machine-readable output, and safe handling of destructive operations in both interactive and scripted use. Read [references/cli.md](references/cli.md) when designing or reviewing a CLI.

## Respect attention and autonomy

Interruptions are expensive: people often take many minutes to return to an interrupted task, and some never do. Interrupt only in proportion to honest urgency, let people control channels and frequency, batch what can wait, and help people resume where they left off.

Design for informed, free decisions. Make leaving as easy as joining and declining as easy as accepting, present options with comparable prominence, stop asking once someone has answered, and disclose costs and terms before commitment. Patterns that deceive, pressure, or obstruct, such as hidden costs, preselected upsells, confirmshaming, fake urgency, and cancellation mazes, violate this line and increasingly violate consumer-protection and platform law. Surface the conflict to the user when a request asks for one.

## Build accessibility into the component definition

Accessibility is stricter interaction design, and it helps everyone using touch, low light, fatigue, or imprecise input. Use semantic elements before custom widgets, give every control an accessible name, keep a logical focus order with a visible focus indicator, and make every flow operable by keyboard alone. Where an input inherently depends on the path of movement, such as freehand drawing or a drawn signature, provide a keyboard-operable way to reach the same outcome, such as typing a name. Announce non-urgent status changes politely without moving focus, and reserve assertive announcements for urgent problems. Associate field errors and descriptions with their fields.

Size targets for the input method: WCAG 2.2 AA sets a minimum of 24 by 24 CSS pixels with spacing exceptions, while touch platforms commonly recommend around 44 points. Dragging needs both a click-or-tap alternative and keyboard operability, covered in the patterns reference. Respect reduced-motion preferences, and use motion only to explain spatial relationships, state changes, or shifts of attention, never as a delay before information appears.

## Keep people in control of AI and agents

AI output is probabilistic, so feedback, control, and recovery matter more, not less. Structured UI remains the right tool for deterministic tasks; natural language is an accelerator for ambiguous intent, generation, and transformation. When the product exposes AI features or agent actions, or when AI is generating the interface, read [references/ai-interaction.md](references/ai-interaction.md).

## Verify by walking the flows

Judge an interface by what happens when people use it, not by how a screenshot looks. Choose the checks the change can affect, translated to the interface type; for a CLI, keyboard and focus checks become interactive and non-interactive runs, piped output, and exit codes: walk the primary task as a first-time user; complete it by keyboard alone; simulate slow responses, empty data, network failure, timeouts with unknown outcomes, permission denial, and partial failure; trigger each error and check that recovery works; confirm that destructive and side-effecting actions show their consequences and can be undone or were confirmed; and, for AI features, check that a wrong result can be corrected locally without starting over. Use automated accessibility checks where available, but a passing scan does not prove operability.

When implementation is in scope, run the interface and observe these states rather than inferring them from code. When only a design or review is possible, state which scenarios remain unverified and what evidence would settle them.

For a written interaction specification, use [templates/INTERACTION-SPEC.md](templates/INTERACTION-SPEC.md). For a written review, use [templates/INTERACTION-REVIEW.md](templates/INTERACTION-REVIEW.md).

## Done when

Scope each condition to the flows and states the change touches.

For design, the users, tasks, and objects involved are explicit; each affected flow has its states, feedback, error handling, and recovery defined; destructive and side-effecting actions have a prevention, confirmation, or undo policy that the backend can honor; the trade-offs chosen between competing principles are stated; frequent tasks have both a visible path and an accelerator; and accessibility requirements are part of each component rather than a later pass.

For review, each finding describes a concrete user, action, and failure; is ranked by frequency, impact, and persistence; is labeled as observed behavior or heuristic prediction; and proposes a fix that follows existing conventions or states the evidence for departing from them.

For implementation, the specified states can be observed in the running interface, the affected tasks complete with the relevant input methods and under the slow or failing conditions they can meet, without data loss, and any scenario that could not be exercised is reported instead of assumed.
