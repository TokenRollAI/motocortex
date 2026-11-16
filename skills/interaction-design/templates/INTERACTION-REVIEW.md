# Interaction Review Template

Write in the user's language, keeping only concrete findings backed by a specific persona, action, and failure mechanism. Rank by `frequency x impact x persistence`, and label evidence class (`observed | measured | predicted`) explicitly so heuristic predictions are never passed off as runtime observations.

<interaction-review-template>
# [Feature or Surface]: Interaction Review

[Reviewed scope, build/revision, platforms/viewports, target personas and tasks, and evidence basis: live walkthrough, telemetry, usability sessions, or heuristic inspection]

## Executive judgment

[The 2-3 highest-impact issues governing task completion, error risk, or operator speed, and the overarching recommendation.]

## Ranked findings

### [S4 | S3 | S2 | S1] [Crisp problem statement]

- Evidence: [`observed` | `measured` | `predicted`] — [repro trace, screenshot/command, or metric]
- Persona and trigger: [who hits this, during which task and state]
- Failure and cost: [what breaks, stalls, bloats the viewport, or misleads, and whether it persists for repeat users]
- Root mechanism: [missing state, feature-stacking bloat, density mismatch, AI slop, object mismatch, safeguard imbalance, or affordance gap]
- Fix: [concrete change, subtraction/cut, or copy replacement reusing existing conventions, plus any trade-off accepted]

## Trade-offs and open decisions

[Competing principles balanced by the proposed fixes, user-owned choices required, and the smallest check that settles uncertain predictions.]

## Unverified states

[Reachable states, input modes, viewports, or assistive paths not exercised in this pass and how to verify them.]
</interaction-review-template>
