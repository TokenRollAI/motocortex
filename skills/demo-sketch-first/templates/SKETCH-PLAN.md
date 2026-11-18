# Feature or Architecture Sketch Plan Template

Share a compact plan like this before writing large TSX stages when feature framing, interaction alternatives, or data-pipeline scope are still open. Omit sections that do not apply.

<sketch-plan-template>
# Sketch Plan: <Plain capability or architecture question>

## Audience and decision

- Audience: <who is reviewing and what interaction or architectural question they want to settle before coding>
- Goal: <one sentence: actor, surface/caller, and desired outcome — solution-neutral when comparing options>

## Proposed behavior and genuine alternatives

- <Single settled direction (`work()` or 1-option `feature()`): how it behaves visually on screen | key assumption>
- <Or when a real choice is open — **Option A · <Mechanism>** vs **Option B · <Mechanism>**: how each behaves on screen | primary strength | main trade-off>

## User situations or chapters (`cases` for feature options; `chapter()` outcomes for standalone works)

| Key | Situation or chapter title (`Given` / action) | Visible screen outcome (`Then` / `expected`) |
|---|---|---|
| `<key>` | <Plain everyday starting situation or pipeline stage> | <Exact interface state or diagram state visible at the end> |

## Stage, architecture diagrams, and live review

- UI stage (when applicable): <host UI surface, input triggers, state indicators, and before -> after visual change — zero bullet-slide cards>
- Architecture & data pipeline (`@joplo-app/plugin-diagram`, when applicable): <domain groups/stores, payload hops from producer -> transform -> storage -> consumer, `Sequence` / `StateMachine` views, and failure/timeout reconciliation shown>
- Verification & live feedback: `joplo check`, `joplo outline`, `joplo render --sheet` (with `--out` on qualified scenario IDs) + live board walkthrough, and `joplo feedback watch` confirmed listening before sharing the URL
</sketch-plan-template>
