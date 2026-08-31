---
name: architecture-design
description: >-
  Design or review software architecture and technology choices from functional
  goals, quality attributes, constraints, existing system context, and credible
  change vectors. Use when deciding a system or major feature's structure,
  module, service, data, or integration boundaries, technology stack,
  architectural trade-offs, migration or evolution path, or when diagnosing
  over-engineering, weak layering, excessive coupling, or misplaced
  extensibility. Do not use for routine local implementation choices that do
  not materially affect system structure.
---

Architecture is the arrangement, under uncertainty, of **which decisions must be made now and which changes must stay affordable later**. Its value is not more layers or fashionable patterns — it is a system simple enough to meet what actually matters, with expensive change confined behind clear boundaries.

## Start from the driving forces

First understand the business outcomes the system must produce, the critical user paths, the business invariants, and the existing constraints. Turn structure-shaping quality requirements into concrete scenarios: under what load, failure, or change must the system make what observable response. "High performance", "scalable", "highly available" cannot guide design by themselves; only requirements with an environment, a scale, and an outcome can enter a trade-off.

Read the existing code, configuration, docs, dependencies, and runtime environment first. Look up whatever the environment can answer yourself, and prefer continuing technologies and conventions already proven to meet the need. Widen the candidate set only when the current approach shows a clear gap — do not pay migration, learning, and operations costs for theoretical advantages.

Separate ordinary implementation choices from architecturally significant decisions. If the core stack, data ownership, module or service boundaries, consistency model, key integration style, or a hard-to-exit dependency is still open, investigate first and hand the trade-off to the user to settle before advancing the work that depends on it. Decide local, reversible, structure-neutral choices yourself — do not turn everyday development into an architecture meeting.

## Make every structure answer for its cost

Draw boundaries around business invariants, data ownership, independent change, and failure isolation. A boundary's purpose should be stateable as one causal sentence: what rule it protects, what change it isolates, or what failure propagation it stops.

Only a layer that encapsulates policy, transforms a model, shields change, or isolates a dependency has absorbed real complexity. A layer that merely forwards calls, duplicates names, or spreads one modification across more files is hauling complexity around — merge it. Conversely, when business rules, infrastructure, and interface changes keep entangling each other, introduce the boundary that separates them.

Treat patterns as tools that resolve known forces, never as starting points. Microservices, event-driven designs, DDD, Clean Architecture, plugin systems, or any framework must buy a capability needed now, with the coordination, consistency, debugging, deployment, and cognitive costs accounted for. Choose the simplest complete design that satisfies the forces; adopt nothing because it is popular or familiar.

## Keep extensibility on the credible change frontier

Weigh both how credible a change is and how costly it would be to make later. Known roadmaps, business volatility, external dependencies, regulatory edges, or expensive one-way commitments form a credible change frontier; when both credibility and cost are high, localize the change behind stable interfaces, information hiding, or replaceable boundaries — and state what that flexibility protects.

An imagined future is not a driving force. When a change has no evidence, or refactoring later would be cheap, keep the design simple: no premature generic frameworks, plugin mechanisms, configuration layers, or unused capabilities. Simple is not rigid — clear responsibilities, tests, and low coupling keep later modification affordable without building future features today.

## Choose technology and structure on evidence

Compare only candidates that genuinely stand a chance. Examine them against the current driving forces: capability, team fit, ecosystem and maintenance status, operations and migration cost, interoperability, exit path, and failure impact — not a forced quota of options or a scoring matrix.

Versions, limits, support windows, prices, and ecosystem health change; verify them against current official sources. For assumptions the sources cannot settle but the design's success depends on, validate with a minimal prototype, benchmark, or spike; treat that code as learning material, not production by default. Write the conclusion with the reason for the choice, the costs accepted, and the condition changes that should trigger a re-examination.

Walk the design once along a representative user path, data flow, failure path, and future change. This surfaces synchronous chains, shared state, implicit ownership, and cross-boundary coordination without imposing a mechanical architecture checklist on every project. When a written record is warranted, follow the repository's existing ADR or architecture-doc conventions; if the user has not asked and the repository has none, do not invent a documentation system.

## Done when

Every architecturally significant choice traces to a functional goal, a quality scenario, or a real constraint; technical facts are verified and success-critical unknowns are validated or explicitly exposed; every boundary and layer states the complexity it absorbs; extension points correspond to credible, expensive change, with speculative abstraction excluded; the major costs, exit paths, and re-examination triggers are clear; and every open decision that would change the architecture irreversibly has been handed to the user before the implementation that depends on it begins.
