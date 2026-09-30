# Interaction Specification Template

Use this when the task calls for a written interaction specification. Write it in the user's language, replace placeholders with decisions, cover only the flows and states the change touches, remove sections that do not apply, and keep open questions explicit rather than filling them with guesses. For a CLI, replace the accessibility and responsive sections with output streams, exit codes, machine-readable output, and interactive versus non-interactive behavior. Reference existing design-system components by name instead of redefining them.

<interaction-spec-template>
# [Feature or product]: Interaction Specification

[Scope, platform(s), related existing flows, and the design system or conventions this follows]

## Users and tasks

- Primary users: [who, how often, expertise]
- Primary task: [what they must get done, and what failure costs]
- Secondary tasks: [supporting tasks]
- Expert path: [shortcuts, command palette, bulk actions, automation or API]

## Object model and information architecture

[The user-facing objects, their vocabulary, and how they relate. The navigation path to each object, and what each screen shows about where the user is, what is here, and what they can do next.]

## Primary flows

[For each flow: entry points, steps, the result, and where the user lands afterwards. Note what is preserved across navigation, such as drafts, filters, selection, and scroll position.]

## Action lifecycles

| Action | Immediate feedback | Pending | Success | Failure and recovery | Unknown outcome | Reversibility |
|---|---|---|---|---|---|---|
| [action] | [acknowledgement] | [indicator, scope, duplicate protection] | [confirmation, next step] | [message, data safety, retry or cancel] | [how the outcome is checked, when retry is safe] | [undo, confirm, or preview, and what the backend can reverse] |

## View states

[For each affected view, the reachable states among first use, empty, loading, partial, full, slow, offline, permission-denied, and partial failure, and their behavior.]

## Destructive and side-effecting actions

[Each such action, its impact, and its policy: undo, preview or diff, or explicit confirmation naming the consequence. For agent actions, the approval point and how users pause or stop.]

## Trade-offs

[Principles that conflicted, such as consistency and innovation, density and simplicity, undo and confirmation, or optimistic and pessimistic updates; the choice made and the evidence or assumption behind it.]

## Content

[Key action labels, terminology, error and confirmation wording, and localization constraints.]

## Accessibility

[Semantic structure, accessible names, focus order and visible focus, keyboard operation of every flow, status announcements, field error association, target sizes, non-drag alternatives, reduced motion, and non-color signals.]

## Responsive behavior

[How layout, navigation, and interactions adapt across screen sizes and input methods.]

## AI behavior

[Only if applicable: expectations shown to users, where output lands as an editable object, uncertainty and provenance display, correction actions, and failure handling.]

## Verification scenarios

- [First-time user completes the primary task]
- [Primary task completed by keyboard alone]
- [Slow, offline, empty, permission-denied, and partial-failure behavior]
- [Each error triggered and recovered without data loss]
- [Destructive actions undone or confirmed with named consequence]

## Open questions

[Decisions that still need the user or stakeholders, and what each blocks]
</interaction-spec-template>
