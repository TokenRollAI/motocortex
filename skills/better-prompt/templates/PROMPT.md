# Better Prompt Delivery Template

Include only sections that earn their place for the requested delivery. Place copy-ready instructions in the appropriate system/developer/user layer, and keep runtime configuration and evals outside the prompt text itself.

<better-prompt-template>
# Optimized Prompt

## Objective

[Outcome to achieve, target audience/caller, and what defines a complete result.]

## Context and trust boundaries

[Inputs provided, authoritative sources vs untrusted external data, and environmental facts.]

## Invariants and constraints

- [Non-negotiable factual, scope, safety, or authorization rule — plus the causal reason it matters and fallback behavior when blocked.]

## Decision criteria (optional)

[How to weigh competing priorities, when to act autonomously vs ask, and when to stop; prescribe step order only where order itself is mandatory.]

## Output contract

[Required structure, precision/density, tone, and language — deferring strict syntax to runtime schemas where applicable.]

## Examples (optional)

[Include only minimal boundary examples needed to disambiguate subtle format, label, or tone edges.]

# Runtime Notes (outside prompt)

- Target model & reasoning config: [model ID / portable target, thinking budget]
- Schemas & tool contracts: [constraints owned by JSON Schema, validators, or tool definitions]
- Caching & context layout: [static prefix vs dynamic tail]

# Validation Cases

| Slice | Input trigger | Pass invariant | Regression / failure signal |
|---|---|---|---|
| Core path | [representative real task] | [expected behavior] | [observable failure] |
| Hard boundary | [edge or conflicting constraint] | [expected trade-off resolution] | [observable failure] |
| Missing ground truth | [omitted prerequisite fact] | [targeted question or explicit narrowing] | [silent fabrication or overreach] |
| Domain hazard | [highest-risk failure mode] | [guardrail behavior] | [unauthorized action or corruption] |

# Delta Summary

- Preserved: [load-bearing intent and effective rules kept]
- Cut: [redundant, conflicting, or legacy scaffolding removed]
- Tightened: [invariants or layer fixes introduced]
- Unverified: [hypotheses pending live eval on target runtime]
</better-prompt-template>
