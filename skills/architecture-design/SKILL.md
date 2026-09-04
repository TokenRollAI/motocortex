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

Match the depth and output to the request: a focused review may need a few findings, while a new system may need a design and supporting experiments. Use the following lenses where they can change the conclusion. A review request does not itself authorize restructuring the system.

## Start from the driving forces

First understand the business outcomes the system must produce, the critical user paths, the business invariants, and the existing constraints. Turn structure-shaping quality requirements into concrete scenarios: under what load, failure, or change must the system make what observable response. "High performance", "scalable", "highly available" cannot guide design by themselves; only requirements with an environment, a scale, and an outcome can enter a trade-off.

Inspect the existing code, configuration, docs, dependencies, and runtime context relevant to the decision. Look up discoverable facts yourself, and prefer continuing technologies and conventions already proven to meet the need. Widen the candidate set when the current approach shows a gap; theoretical advantages alone rarely repay migration, learning, and operations costs.

Separate ordinary implementation choices from architecturally significant decisions. For open choices about the core stack, ownership, boundaries, consistency, integration, or hard-to-exit dependencies, explain the trade-off and identify whether the user's existing instructions settle it or delegate it. Bring unresolved user-owned choices back before committing dependent implementation. Decide local, reversible, structure-neutral choices yourself so architectural attention stays on costly commitments.

## Make every structure answer for its cost

Draw boundaries around business invariants, data ownership, independent change, and failure isolation. A boundary's purpose should be stateable as one causal sentence: what rule it protects, what change it isolates, or what failure propagation it stops.

Assess a layer by the policy, model transformation, change, or dependency it isolates. Forwarding calls alone does not justify its cost, but an apparently thin interface may still protect a real ownership or compatibility boundary. Recommend consolidation when the indirection adds cost without protecting a relevant constraint; introduce separation when business rules, infrastructure, and interface changes repeatedly interfere. Apply structural changes within the task's scope.

Treat patterns as tools that resolve known forces, never as starting points. Microservices, event-driven designs, DDD, Clean Architecture, plugin systems, or any framework must buy a capability needed now, with the coordination, consistency, debugging, deployment, and cognitive costs accounted for. Choose the simplest complete design that satisfies the forces; adopt nothing because it is popular or familiar.

## Keep extensibility on the credible change frontier

Weigh both how credible a change is and how costly it would be to make later. Known roadmaps, business volatility, external dependencies, regulatory edges, or expensive one-way commitments form a credible change frontier; when both credibility and cost are high, localize the change behind stable interfaces, information hiding, or replaceable boundaries — and state what that flexibility protects.

An imagined future is not a driving force. When a change has no evidence, or refactoring later would be cheap, keep the design simple: no premature generic frameworks, plugin mechanisms, configuration layers, or unused capabilities. Simple is not rigid — clear responsibilities, tests, and low coupling keep later modification affordable without building future features today.

## Choose technology and structure on evidence

Compare only candidates that genuinely stand a chance. Examine them against the current driving forces: capability, team fit, ecosystem and maintenance status, operations and migration cost, interoperability, exit path, and failure impact — not a forced quota of options or a scoring matrix.

Versions, limits, support windows, prices, and ecosystem health change; verify them against current official sources. For assumptions the sources cannot settle but the design's success depends on, validate with a minimal prototype, benchmark, or spike; treat that code as learning material, not production by default. Write the conclusion with the reason for the choice, the costs accepted, and the condition changes that should trigger a re-examination.

Use representative user paths, data flows, failures, or credible changes to test the boundaries most likely to fail. Such examples expose shared state, implicit ownership, and coordination that a structural diagram can hide; select the ones relevant to the decision. When a written record is warranted, follow existing ADR or architecture-doc conventions; otherwise deliver the reasoning in the form the task needs.

## Done when

The design, recommendation, or review answers the requested architectural question. Significant choices and boundaries trace to relevant goals or constraints; technical claims have evidence, and success-critical unknowns are validated or exposed with their implications. The main costs, credible change needs, and conditions for reconsideration are clear. Any user-owned decision needed before implementation is identified without turning completion of the review into an implementation requirement.
