# Better Prompt Delivery Template

Use only sections that help the requested delivery. Replace placeholders with task content; the guidance in this paragraph is for the author, not part of the resulting prompt. Place instructions in the appropriate system, developer, or user layer for the target runtime, and keep runtime notes and evals outside the copy-ready prompt.

<better-prompt-template>
# Optimized Prompt

## Goal

[the outcome the user should see]

## Context

[the minimum background, input definitions, and boundaries needed to complete the task]

## Success criteria

- [observable or verifiable completion conditions]

## Constraints

- [necessary business, factual, scope, or authorization constraints and why they matter]

## Judgment (optional)

[trade-offs, relevant conditions, and evidence that should guide choices; prescribe a sequence only where the sequence itself is required]

## Output

[content, structure, length, audience, and language requirements]

## Role and collaboration (optional)

[only a short note that changes the professional lens, tone, or collaboration behavior]

## Evidence and tools (optional)

[source standards, tool-selection conditions, data boundaries for inputs and tool returns]

## Authority and approval (optional)

[actions allowed autonomously, side effects requiring confirmation, scope boundaries]

## Verification and stop rules (optional)

[verification method, retry/fallback conditions, when to ask or stop]

## Examples (optional)

[only the minimal examples that fix known boundary, format, or style failures]

# Runtime Notes (outside the prompt)

- Model: [target model, or "keep portable"]
- Reasoning / thinking: [suggested value and the baseline to compare against]
- Verbosity / output control: [runtime settings]
- Structured output / tool schema: [constraints the API or a validator should own]
- Context / caching: [static prefix, dynamic input, and compression advice]

# Minimal Evals

| Case | Input characteristics | Expected behavior | Failure signal |
|---|---|---|---|
| Normal path | [typical input] | [core success criterion] | [observable failure] |
| Boundary path | [hard case or extreme value] | [boundary behavior] | [observable failure] |
| Insufficient information | [missing key field] | [ask, narrow, or decline] | [guessing or overreach] |
| Domain risk | [the domain's key risk] | [safety/quality behavior] | [risk event] |

# Change Notes

- Kept: [the parts of the original prompt that were effective and necessary]
- Removed: [duplicated, conflicting, outdated, or ineffective scaffolding]
- Added: [minimal constraints added for identified failure modes]
- Pending validation: [assumptions without evidence, to be evaluated on the target model]
</better-prompt-template>
