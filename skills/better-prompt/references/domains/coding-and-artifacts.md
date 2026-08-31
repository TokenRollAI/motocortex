# Coding and Artifacts

Applies to code, websites, documents, spreadsheets, presentations, images, and other artifacts that must be generated and verified. The prompt should read like a high-quality task brief: clear behavioral goals and acceptance, with room left for the agent to explore the current state and choose the implementation path.

## How to optimize

Lead with the goal, pointers to the current state, scope, invariants, and non-goals. When an existing repository or artifact already has a design system, format, stack, and conventions, require checking and reusing them first — do not rewrite them from thin air inside the prompt.

Write the Definition of Done as runnable tests, builds, type checks, render checks, user scenarios, or human acceptance points. "Self-review" or "high quality" alone cannot serve as completion criteria.

Specify libraries, architecture, or file-level steps only when the implementation path is itself a hard constraint. Otherwise describe behavior, interfaces, compatibility, performance, and security boundaries, and let the model choose the minimal change given the existing context. State explicitly which refactors, extra features, and future abstractions are out of scope.

Separate planning, editing, verification, committing, deployment, and external publication. A request to implement normally authorizes in-scope local edits and non-destructive verification; it does not automatically authorize deployment, opening PRs, sending messages, or other external writes.

Require visual or typographic artifacts to be checked after rendering. Require code to run the most relevant tests; when verification is impossible, report why and the next-best check. Do not let a long explanation substitute for the real artifact and its verification results.

## Minimal evals

- does a typical change satisfy the user scenario;
- is the diff confined to the authorized scope and preserving existing conventions;
- were the tests, build, or render actually run;
- are input anomalies, compatibility, and regression risk covered;
- did the model add features, refactor, or take external actions on its own.

Done when: the deliverable's path is clear, success is verifiable through tools or user scenarios, and both the implementation freedom and the unbreakable invariants are explicit.
