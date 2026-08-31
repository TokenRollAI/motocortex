---
name: better-prompt
description: >-
  Draft, diagnose, or optimize prompts for current high-performance models
  across direct response, reasoning, research, creative, coding/artifact, and
  tool-using agent work. Use when the prompt itself is the artifact or subject
  of diagnosis: a prompt is missing, bloated, brittle, legacy, model-specific,
  underperforming, or needs migration, simplification, or evaluation.
---

Treat a prompt as a **task contract**, not an incantation that unlocks model capability. The goal of optimization is not longer text or a more spec-like look — it is the target model delivering what the user actually wants, reliably, with less ambiguity, fewer conflicts, and fewer dead constraints.

## Preserve the original intent first

The input may be an existing prompt or just a rough goal. Recover its real intent first: audience, inputs, deliverable, success criteria, and where it runs. Distinguish stable system/developer rules, the current user task, external data, and tool returns; do not mash content of different priorities into one blob.

Look up yourself whatever the existing prompt, calling code, tool schemas, evals, or context can answer. Ask only about decisions that would materially change the contract; for the rest, proceed on the most conservative reasonable assumption and list the assumptions outside the prompt for the user to confirm.

Given an existing prompt, preserve its effective behavior and authorization boundaries first, then make the smallest change with the most explanatory power. Given only a rough goal, produce a minimal usable version — do not preempt every failure that has not yet been observed.

## Route by task shape

Determine the dominant task shape first, and read only the relevant domain guide. When one prompt mixes several shapes, read the necessary few and make the priority explicit — do not pile every domain's rules in.

| Task shape | When to read |
|---|---|
| Direct response and text transformation | Q&A, explanation, summarization, extraction, classification, rewriting, translation: read [direct-response.md](references/domains/direct-response.md) |
| Reasoning and decisions | Math, analysis, planning, comparison, recommendation, diagnosis: read [reasoning-and-decisions.md](references/domains/reasoning-and-decisions.md) |
| Research and synthesis | Search, fact-checking, citations, literature or competitive synthesis: read [research-and-synthesis.md](references/domains/research-and-synthesis.md) |
| Coding and artifacts | Code, websites, documents, spreadsheets, presentations, or other verifiable artifacts: read [coding-and-artifacts.md](references/domains/coding-and-artifacts.md) |
| Tool-using agents | Calls tools, changes state, runs long, or handles untrusted external content: read [tool-using-agents.md](references/domains/tool-using-agents.md) |
| Creative work | Ideation, copywriting, stories, visual direction, open-ended design: read [creative-work.md](references/domains/creative-work.md) |

When the user names a model, asks for migration, or the optimization depends on current model capabilities, also read [model-adaptation.md](references/model-adaptation.md) and check that model's current official guidance. When you need to prove an optimization works or design a regression set, read [evaluation.md](references/evaluation.md).

## Diagnose before rewriting

Look for problems that actually change behavior:

- vague goal, inputs, completion criteria, or audience;
- duplicated or conflicting instructions, or every requirement written at top priority;
- steps prescribed that are irrelevant to the goal, narrowing paths the model could validly take;
- only unverifiable demands like "be careful", "be professional", "don't hallucinate";
- context piled up with unclear provenance, or blurred boundaries between data and instructions;
- few-shot examples that fix no known failure and instead anchor wrong patterns;
- runtime controls — reasoning depth, verbosity, temperature, schema — disguised as universal natural-language tricks;
- underspecified tools, permissions, side effects, evidence, verification, retries, and stop conditions;
- expecting the prompt alone to solve permission isolation, structural constraints, or prompt injection.

Sort out the root cause. If a problem belongs to tool design, permissions, retrieval, model choice, runtime parameters, schema, server-side validation, or missing evals, say so explicitly and move it to the right layer — do not paper over a system problem with more prompt text.

## Rewrite into a minimal task contract

Keep the goal, necessary context, success criteria, hard constraints, and delivery format first. Add role, personality, fixed procedures, tool routing, authorization, stop rules, or examples only when they change behavior.

- Describe the destination and let a high-performance model choose its own ordinary reasoning and execution path. Fix steps only when the path itself involves compliance, reproducibility, authorization, or business process.
- State every rule once. Reserve absolutes for true invariants; write judgment calls as conditions and decision criteria.
- Describe expected outcomes as positive, observable behavior. When a prohibition is necessary, state the alternative behavior.
- XML, Markdown headings, or delimiters exist only for boundary clarity; pick one consistent structure and do not treat formatting as a performance secret.
- Use examples only for label boundaries, style, format, or recurring failures that are hard to define in words; keep them minimal, realistic, and mutually consistent.
- Do not ask the model to recite its full hidden chain of thought. Ask for key assumptions, evidence, calculations, verification results, or a concise rationale instead.
- Default to a portable core; put vendor-specific parameters, API schemas, and caching advice outside the prompt.

When a full deliverable is needed, organize it per [templates/PROMPT.md](templates/PROMPT.md). Delete every empty optional module; the template is not a mandate to turn every prompt into a long document. Default to returning a copy-ready result in the conversation; write to a file or replace an existing prompt only when the user asks.

## Validate against failure modes

Do not declare an optimization successful because it "reads more professional". With existing evals, establish a before/after baseline on the same model, runtime parameters, and samples; without evals, at least provide a minimal test set covering a normal input, a boundary input, an insufficient-information case, and one domain-specific risk.

Change one meaningful module at a time and compare task success, factual and constraint correctness, format, cost, latency, tool-call counts, and failure types. Model self-assessment can surface problems, but it cannot replace tests, validators, source verification, or human preference judgment.

## Done when

The deliverable preserves the user's original intent and authorization boundaries; the core prompt is directly usable, free of duplication and conflict, and contains only behavior-changing modules; domain-specific risks are handled; runtime configuration is separated from the prompt; and a minimal eval suggestion sufficient to validate the change is provided. If no eval has run on the target model, mark the result "pending validation" — do not claim it is already better.
