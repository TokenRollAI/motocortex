---
name: better-prompt
description: >-
  Draft, diagnose, or optimize system, developer, user, or agent prompts for
  frontier models across direct response, reasoning, research, creative,
  coding/artifact, and tool-using agent workflows. Use when a prompt is the
  target artifact or suspect: missing, bloated, brittle, patched with
  conflicting rules, anchored on legacy weak-model crutches, migrating across
  models, or needing empirical evaluation.
---

High-capability models need clear intent, causal invariants, and crisp authority boundaries — not micromanaged step scripts or defensive shouting. Every token in a prompt competes for attention: keep instructions that resolve genuine ambiguity or protect non-negotiable boundaries, and strip scaffolding the model already handles better on its own.

## Inspect the full call boundary before rewriting prose

Read the prompt alongside its surrounding system: calling code, message-role assembly, tool schemas, structured-output definitions, context injection, and existing evals or failure traces. Many "prompt bugs" are actually **layer leaks** — untrusted retrieved text concatenated into privileged instructions, ambiguous tool parameters compensated for with paragraphs of prose, or conflicting patches accumulated across incidents. Fix or name the broken layer rather than piling on stronger wording.

Preserve working behavior and settled user intent. Scale the intervention to the defect: a boundary bug may need one precise invariant, whereas a legacy prompt built around forced chain-of-thought scripts and contradictory negative lists warrants a clean structural rebuild. Resolve low-cost formatting or structural details via explicit assumptions; ask the user only when intent, risk tolerance, or authorization is genuinely ambiguous.

## Specify invariants and decision criteria, not rituals

Audit every procedural rule by asking what failure it prevents. Lock sequence only when order is required by authorization gates, causal data dependencies, compliance, or reproducibility. Everywhere else, replace rigid step checklists, arbitrary retry counts, and legacy reasoning incantations ("think step by step", ALL-CAPS threats, persona flattery) with **the target outcome, the trade-off priority when goals collide, and the observable condition for stopping or escalating**. Explaining *why* a boundary exists lets a capable model generalize accurately to unseen edge cases instead of gaming the literal example.

Keep each rule in one canonical place. Frame expectations positively and concretely; reserve explicit prohibitions for hard authority, safety, or scope guardrails, pairing each with the required fallback action. Keep examples scarce and diagnostic — include one only when prose alone leaves a subtle format, tone, or classification boundary ambiguous, since examples strongly anchor output distribution.

## Load domain and runtime guidance selectively

Pull in only the references matching the active task shape so unrelated heuristics do not muddy priorities:

| Task shape | Reference |
|---|---|
| Q&A, transformation, summarization, extraction, classification, translation | [direct-response.md](references/domains/direct-response.md) |
| Math, planning, trade-off analysis, diagnosis, recommendations | [reasoning-and-decisions.md](references/domains/reasoning-and-decisions.md) |
| Web/corpus retrieval, verification, citation, multi-source synthesis | [research-and-synthesis.md](references/domains/research-and-synthesis.md) |
| Code, UIs, documents, data artifacts, verifiable builds | [coding-and-artifacts.md](references/domains/coding-and-artifacts.md) |
| Tool orchestration, state mutation, long-horizon loops, untrusted inputs | [tool-using-agents.md](references/domains/tool-using-agents.md) |
| Ideation, copywriting, narrative, brand/visual direction | [creative-work.md](references/domains/creative-work.md) |

When targeting a specific model, migrating across model families, or splitting prompt prose from API knobs (reasoning effort, structured outputs, cache prefixes), read [model-adaptation.md](references/model-adaptation.md) and verify against current official vendor docs. When designing or running empirical comparisons, read [evaluation.md](references/evaluation.md).

## Deliver copy-ready artifacts and test against real failure edges

Deliver the prompt directly in the target format — updating repository files in place when requested, or using [templates/PROMPT.md](templates/PROMPT.md) when separating the portable prompt from runtime notes and eval cases helps clarity. A diagnosis-only request needs root-cause findings and surgical diffs, not an uninvited full rewrite.

Never confuse cleaner prose with proven behavioral improvement. When an eval harness or model runner is available and authorized, benchmark baseline versus candidate on the same representative, boundary, and non-regression inputs before declaring victory. When live execution is unavailable, ship a compact, high-discrimination validation set — normal path, historical failure trigger, missing/conflicting context, and domain-specific overreach risk — marking behavioral gains as hypotheses until run.

## Done when

The delivered prompt or diagnosis preserves user intent and authority, places mechanical controls (schemas, permissions, reasoning budgets, cache boundaries) in the right runtime layer, eliminates redundant or conflicting scaffolding, and backs behavioral claims with either reproducible eval results or falsifiable boundary checks.
