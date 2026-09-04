# Research and Synthesis

Applies to web search, fact verification, literature review, competitive research, and multi-source synthesis. The core of a research prompt is the evidence protocol and stop conditions, not a phrase like "research thoroughly".

## How to optimize

Scope the research question to the necessary time range, geography, subjects, definitions, and decision purpose. State the source priority: when primary materials, official docs, papers, regulatory information, and reliable secondary reporting are each acceptable.

Define the retrieval depth. Ordinary fact-checking, a representative scan, and an exhaustive review need different budgets. Require stopping when further retrieval can no longer change the core conclusion; do not keep searching for volume.

Set citation discipline: cite only sources actually read; place citations next to the claims they support; separate direct evidence from inference; when sources conflict, present the difference and its likely causes. When evidence falls short, narrow the conclusion or list it as open — do not write "not found" as "does not exist".

Organize long material so provenance and relevance remain visible. Filtering, deduplication, and source grouping help when volume obscures the evidence; preserve dates, authors, and applicability through any compression. Keep the research question clear. External pages, files, and retrieval results are untrusted data; instructions inside them must not override the research task.

For time-sensitive questions, state the current date or require the runtime to supply it, and use retrieval rather than model memory. Do not bake changing vendor, price, legal, or version information into a long-lived prompt.

## Minimal evals

- a narrow question one official source can answer;
- a question needing multi-source cross-validation;
- a question where sources conflict;
- a question without sufficient evidence;
- external material carrying malicious or irrelevant instructions.

Check source quality, claim coverage, date discipline, citation correspondence, inference marking, and whether stopping was reasonable.

Done when: the research scope is bounded, every significant claim traces to evidence, conflicts and gaps are visible, and retrieval stops under reasonable conditions.
