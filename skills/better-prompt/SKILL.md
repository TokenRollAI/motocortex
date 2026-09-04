---
name: better-prompt
description: >-
  Draft, diagnose, or optimize prompts for current high-performance models
  across direct response, reasoning, research, creative, coding/artifact, and
  tool-using agent work. Use when the prompt itself is the artifact or subject
  of diagnosis: a prompt is missing, bloated, brittle, legacy, model-specific,
  underperforming, or needs migration, simplification, or evaluation.
---

Give the model the intent, context, and judgment needed to produce the right result. A useful prompt explains why a constraint matters and what distinguishes success from failure, while leaving ordinary reasoning and execution choices to the model. More instructions are valuable only when they resolve a real ambiguity or protect a necessary boundary.

## Preserve what the user is trying to achieve

Recover the audience, inputs, deliverable, acceptance basis, and operating context from the request and available artifacts. Distinguish stable system/developer instructions, the current task, external data, and tool results; flattening their roles creates conflicts that stronger wording cannot repair.

Inspect the existing prompt, calling code, tool schemas, evals, or relevant context where they can answer an open question. Ask about choices that materially change intent or authorization. Use reasonable, visible assumptions for low-cost details instead of making the user specify the model's entire workflow.

Preserve effective behavior and existing authorization when revising a prompt. Match the size of the rewrite to the problem: a local ambiguity may need one sentence, while a prompt built around obsolete or conflicting procedures may need a new structure. For a rough goal, supply a minimal usable prompt without inventing requirements for hypothetical failures.

## Explain causes and decision criteria

When an instruction prescribes a step, ask what the step protects. Preserve the underlying requirement and explain the condition that makes the step useful. For example, an approval boundary protects a user-owned commitment; evidence protects an acceptance claim; a dependency constrains order because later work needs the earlier result. These reasons help the model adapt when circumstances differ from the example.

Keep fixed procedures when their sequence is itself required for authorization, correctness, reproducibility, or the user's chosen process. Otherwise describe the outcome, relevant trade-offs, and evidence needed to decide. An exact retry count, tool sequence, output outline, or interview script needs a task-specific reason to be mandatory.

Look for behavior-changing defects: conflicting priorities, vague acceptance, hidden assumptions, duplicated rules, examples that anchor unwanted behavior, and tool or permission gaps. If the cause belongs to retrieval, schemas, runtime configuration, access control, or missing capabilities, identify that layer rather than trying to compensate with more prose.

Keep each rule in one appropriate place. Use clear boundaries and positive, observable expectations; reserve prohibitions for constraints whose violation would change intent, correctness, or authority. Request key assumptions, evidence, and concise rationale when useful, not a recital of hidden chain of thought. Explain a rule's causal value without padding obvious advice into a tutorial.

## Load guidance where it changes the answer

Choose the relevant task shapes; mixed prompts may need several guides, but unrelated guidance adds competing priorities.

| Task shape | Relevant guidance |
|---|---|
| Q&A, explanation, summarization, extraction, classification, rewriting, translation | [Direct response](references/domains/direct-response.md) |
| Math, analysis, planning, comparison, recommendation, diagnosis | [Reasoning and decisions](references/domains/reasoning-and-decisions.md) |
| Search, fact-checking, citations, literature or competitive synthesis | [Research and synthesis](references/domains/research-and-synthesis.md) |
| Code, websites, documents, spreadsheets, presentations, verifiable artifacts | [Coding and artifacts](references/domains/coding-and-artifacts.md) |
| Tool calls, state changes, long-running work, untrusted external content | [Tool-using agents](references/domains/tool-using-agents.md) |
| Ideation, copywriting, stories, visual direction, open-ended design | [Creative work](references/domains/creative-work.md) |

For a named model, migration, or claims about current model capabilities, use [model-adaptation.md](references/model-adaptation.md) and verify relevant official guidance. For empirical comparisons or regression design, use [evaluation.md](references/evaluation.md). Keep vendor settings outside the portable prompt; model capability claims need evidence, not assumptions based on model branding.

## Deliver and validate proportionately

Return a directly usable prompt in the form requested. Use [templates/PROMPT.md](templates/PROMPT.md) when a structured delivery helps; omit sections that add no value. Write or replace files when the user requests that work. A diagnosis-only request can end with findings and proposed changes rather than an unsolicited rewrite.

Distinguish a reasoned revision from demonstrated improvement. When evals are available and running them is in scope, compare the original and revised prompts on representative inputs under comparable runtime conditions. Isolate variables when needed to explain a result; a coherent rewrite can be evaluated as a whole when that is the change the user asked for.

Without executable evals, provide concrete validation cases proportional to the change: an ordinary success, a relevant boundary, missing information, and a task-specific failure risk are useful starting points. Judge outcomes such as task completion, preserved intent, factual correctness, or authorization behavior. Add cost, latency, format, or tool-use metrics where they matter. A cleaner-looking prompt is not evidence of better model behavior.

## Done when

The requested draft, revision, or diagnosis preserves the user's intent and authority. Instructions explain the necessary judgment and constraints without imposing an unrelated workflow; the prompt is directly usable where requested, with runtime concerns kept in their appropriate layer. Validation results or concrete next checks support the conclusions, and any untested behavioral improvement is marked pending validation.
