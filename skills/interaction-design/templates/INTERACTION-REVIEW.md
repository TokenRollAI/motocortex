# Interaction Review Template

Use this when the task calls for a written interaction review. Write it in the user's language, replace placeholders with findings, and keep only findings with a concrete user, action, and failure. Order findings by severity. Label every finding by its evidence so predictions are not mistaken for observations.

<interaction-review-template>
# [Feature or product]: Interaction Review

[Scope reviewed, build or design version, platforms, primary users and tasks assumed, and the evidence available: heuristic inspection, running build, usability sessions, analytics, or support data]

## Summary

[The few problems that most affect task completion or risk, and the overall recommendation.]

## Findings

### [Short problem statement]

- Severity: [0 to 4] because [frequency, impact, persistence]
- Evidence: [observed | measured | predicted], [what supports it]
- Who and when: [user, task, and the situation in which it occurs]
- What happens: [the concrete failure, confusion, or risk]
- Likely cause: [the principle or mechanism involved]
- Recommended fix: [change that follows existing conventions, and its cost or trade-off]

## Trade-offs and open questions

[Conflicting principles the fix must balance, decisions that need the user or stakeholders, and what evidence would settle each.]

## Not verified

[Scenarios, states, platforms, or assistive technologies that were not exercised, and how to verify them.]
</interaction-review-template>
