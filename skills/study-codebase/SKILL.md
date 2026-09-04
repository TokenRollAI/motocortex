---
name: study-codebase
description: >-
  Study a repository through source evidence to explain its purpose,
  architecture, important dependencies, core implementation, and transferable
  design lessons. Use when learning an open-source project, tracing how its
  central mechanism works, preparing a codebase study or learning Gist, or
  extracting a small implementation exercise from an existing system.
  Do not use for routine code navigation, bug fixing, or architecture redesign.
---

Help the reader understand a project well enough to explain its central mechanism and try building a small version of it. Optimize for a few supported conclusions with causal explanations: a directory tour or a list of patterns does not establish how the system works.

## Establish the subject and learning focus

Resolve the repository, revision, and any subsystem or learning question from the request and available context. Inspect discoverable facts yourself; ask only when competing targets or consequential choices prevent useful progress. With no narrower focus, study the project's main user-facing capability. For a large monorepo, explain the overall shape and select the subsystem that implements that capability, stating the coverage boundary.

Record the source URL, inspected commit, and relevant local differences so the report describes an identifiable implementation. Use an isolated checkout when remote source must be obtained. Preserve the target repository; a study does not itself authorize source changes or running setup scripts. Read relevant examples and tests, and execute a focused example only when it materially resolves uncertainty and fits the environment and authorization.

## Build an explanation from evidence

Use the README and project documentation to establish intended purpose and vocabulary, then test that account against entry points, configuration, manifests, implementation, and relevant tests. Follow existing repository navigation guidance. Expand the search along calls, data, and ownership boundaries when a missing connection could change the explanation; exhaustive file coverage is not the goal.

Choose a representative input or user action and trace it from the public entry point through the mechanism that produces the result. Explain the important intermediate representations, state transitions, algorithms, and invariants. Include a failure or boundary case where it reveals why the mechanism is structured this way. Locate the core by causal responsibility, even when it spans several modules or lives in a dependency; a directory named `core` is only a navigation hint.

Describe architectural boundaries through responsibilities, state ownership, and control or data flow. Use a compact diagram when it clarifies those relationships, and connect its important nodes and edges to inspected source. Explain where the project supplies its own policy and where it delegates work to frameworks, libraries, external services, or generated code.

Select dependencies that shape the main capability, boundaries, or development model. For each, explain its role and actual integration point, using manifests or lockfiles for declared or resolved versions and source usage for behavior. Distinguish runtime dependencies from build and test tooling. Trace third-party internals only when understanding the core requires it; use source or official documentation matching the inspected version, and label any remaining boundary as uninspected.

Keep conclusions traceable to inspected evidence while letting the explanation carry the main text. Group supporting source links by mechanism or lesson in a short appendix that doubles as a reading route. Use an occasional inline reference when a precise, surprising, or disputed claim benefits from immediate verification; avoid attaching file-and-line citations to every sentence or trace step. Give links descriptive labels that explain what they support. Pin source links to the inspected commit, adding line ranges only when they help locate a specific implementation; verify the remote and revision rather than inventing URLs. For unavailable remote source or uncommitted changes, use honest local path and symbol references in the appendix and state that limitation.

Distinguish observed implementation, documented intent, inferred rationale, and unknown behavior in the explanation itself. A test read establishes what it asserts; claim a passing test or measured property only after observing the result. Moving citations out of the main text should preserve the connection between important conclusions and their evidence.

## Extract lessons the reader can use

For each worthwhile lesson, explain the problem or constraint, the concrete mechanism, its benefit, its cost, and the conditions under which it transfers. Ground the lesson in the implementation just traced. Present author intent as fact only when a design record or other primary source supports it; otherwise identify the explanation as an inference. Prefer a small number of specific insights over generic praise for modularity, scalability, or clean code.

Turn the strongest lesson into a proposed small implementation exercise. Preserve the mechanism and the invariant that makes it instructive while stripping away unrelated product features and infrastructure. Define an input, expected output, minimum components, deliberate omissions, and an observable check that would reveal whether the mechanism was understood. Mark the exercise as a proposal, and carry forward a user-specified learning focus. Implement it only when requested; preparing a study should leave the reader ready for that next task.

## Deliver a durable study

Write a standalone Markdown note in the user's language using [templates/STUDY.md](templates/STUDY.md). Lead with the central conclusions and develop a connected explanation of the architecture and core behavior. Introduce components by their role before naming implementation symbols, explain necessary terms on first use, and follow a concrete example through the mechanism so the reader can understand it without opening the repository. Use diagrams or short, explained pseudocode when they make a difficult transition easier to grasp. Keep tables for useful comparisons rather than using them as the default form for a walkthrough.

Put the optional source reading route and supporting references at the end, ordered by explanatory dependency. Expose gaps that could change the conclusions, and keep commands, logs, and peripheral inventories out unless they help reproduce an important finding. Read the main text as if its links were unavailable: it should still explain what happens, why the design helps, and what it costs. Repair missing explanations rather than relying on a citation to teach the mechanism.

Save the note to the user's chosen location or an artifact directory outside the studied checkout, using a project-specific filename. Keep an existing unrelated note intact. Check the trace, citations, diagrams, and consistency between claims and evidence before delivery.

A request to create a GitHub Gist authorizes publishing the completed note within the stated scope; reuse that authorization without adding a second approval ceremony. Automatic skill selection for a study alone does not authorize publishing. When Gist delivery is requested, follow [references/gist-publishing.md](references/gist-publishing.md), then return the verified URL, visibility, and local artifact path. If publication is blocked, preserve the completed note and report the specific missing capability or authorization; a local draft is not a published Gist.

## Done when

The note explains the project's purpose, architecture and important dependencies, core behavior, and transferable lessons in natural language that remains understandable without following source links. Important conclusions remain traceable to evidence from the identified revision, with most references collected in the appendix. A representative trace reaches the implementation responsible for the result, or clearly marks the unavailable segment and its effect on confidence. The reader has a useful source reading route and a bounded implementation exercise with observable acceptance. The local artifact is complete, and any requested Gist has been retrieved and checked against it; unresolved research or publication blockers are reported without claiming full completion.
