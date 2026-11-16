# Codebase Study Template

Write in the user's language as clear, connected technical prose that stands on its own without opening links. Strip author instructions, keep epistemic labels (`inspected`, `executed`, `documented`, `inferred`) honest, and collect commit-pinned source links in the final reading route. Use diagrams or simplified pseudocode only where they clarify a non-obvious state transition or invariant.

<codebase-study-template>
# [Project]: Codebase Study

[Repository URL, pinned commit SHA, local/dirty state if any, study date, and subsystem scope]

## Core thesis

[2-4 sentences stating what problem the system solves, the central mechanism/invariant that makes it work, and its most transferable engineering trade-off.]

## Problem and scope

[Target user/caller, concrete input-to-output example, and the deliberate scope boundary separating this system from adjacent tools in its category.]

## Architecture and dependency seams

[How load-bearing components divide state ownership and control/data flow, introduced by job before symbol name. Include a compact topology diagram only if helpful. Distinguish policy implemented here from capabilities delegated to key runtime dependencies (with version/call-site grounding in the appendix), separating runtime deps from build/test tooling.]

## End-to-end mechanism walkthrough

[Follow one concrete operation from public entry point to final effect in connected prose: data structures, state transitions, invariants upheld at each seam, and why each step exists.]

[Trace one revealing boundary, contention, or failure case showing how the design preserves or degrades its invariant — distinguishing static source inspection from executed verification.]

## Transferable design lessons

[For each high-signal lesson: forcing constraint -> concrete mechanism -> benefit bought -> cost accepted -> when to adopt vs avoid. Flag inferred author intent explicitly.]

## Proposed mini-implementation

[A self-contained build proposal isolating the central mechanism and invariant — marked clearly as a proposal.]

- Input -> expected output: [concrete test case]
- Minimal components: [smallest coherent structure]
- Core invariant: [what must hold under stress and why]
- Deliberate cuts: [production features/infra stripped away]
- Falsifiable acceptance check: [happy path + one boundary probe that breaks a naive clone]

## Blind spots and open questions

[Uninspected third-party internals, doc-vs-code discrepancies, or unexecuted runtime assumptions that bound confidence, and what check would settle each.]

## Appendix: Source reading route

[Dependency-ordered reading path supporting the claims above, using descriptive links pinned to the inspected commit SHA (with line ranges only where they sharpen lookup).]

1. [Descriptive commit-pinned link] — [invariant or transition it establishes and what to inspect]
2. [Descriptive commit-pinned link] — [next causal link in the trace]
</codebase-study-template>
