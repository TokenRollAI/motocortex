# Coding and Artifacts

Covers software changes, web interfaces, documents, spreadsheets, slides, and other buildable deliverables. Write the prompt like a senior engineering brief: crisp behavioral invariants and executable acceptance, leaving codebase exploration and local implementation mechanics to the agent.

## Specify contracts, reuse boundaries, and runnable proof

Point the agent to authoritative repo context (existing architecture, design tokens, schemas, conventions) rather than pasting stale copies into the prompt, and require reusing established patterns unless the task explicitly replaces them. Constrain libraries or file paths only when external compatibility demands it; otherwise specify observable behavior, edge/error semantics, performance/security bounds, and explicit non-goals (no drive-by refactors, speculative abstractions, or unrequested features).

Define completion through real execution — unit/integration suites, typechecks, builds, CLI runs, or live render/browser walkthroughs — never "self-review" prose. State authority boundaries clearly (local edits and tests vs commits, pushes, deployments, or external mutations) so authorized work flows uninterrupted without redundant permission prompts. When an environment blocks a check, require naming the exact skipped verification rather than implying pass.

## Discriminating checks

Verify end-to-end scenario completion, diff containment within scope and repo conventions, actual execution of build/test/render verification, edge and regression handling, and absence of unrequested features or abstractions.
