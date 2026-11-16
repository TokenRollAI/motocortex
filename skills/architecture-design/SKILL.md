---
name: architecture-design
description: >-
  Design or review software architecture and technology choices from business
  invariants, workload scenarios, state ownership, constraints, and credible
  change vectors. Use when defining system or module structure, service, data,
  or integration boundaries, consistency and failure semantics, technology
  selection, or migration paths, or when diagnosing over-engineering, leaky
  abstractions, tight coupling, or speculative extensibility. Do not use for
  routine local implementation edits that leave boundaries and contracts intact.
---

Architecture decides **which commitments lock in now and which changes stay cheap later**. Its job is the simplest structure that upholds real invariants and workload demands while containing costly change behind crisp boundaries — never extra layers, single-implementation interfaces, or fashionable patterns added for symmetry.

Scale depth and output to the ask: a targeted boundary review needs sharp causal findings without unsolicited refactoring, whereas a new subsystem may require an end-to-end design and a throwaway validation spike.

## Anchor on invariants, state authority, and concrete scenarios

Extract the business invariants that must never break, the critical user and data paths, who owns writes and truth for each piece of state, and the hard operational constraints. Translate vague quality labels ("scalable", "resilient", "low-latency") into falsifiable scenarios: stimulus, scale or failure mode, and required observable response.

Inspect the live codebase, schemas, deployment topology, and dependencies before proposing structure. Reuse proven stack primitives and platform capabilities first; depart from them only where current capabilities demonstrably fail a driving force, since migration and operational tax are real and theoretical elegance rarely pays them back.

Separate irreversible structural forks (core stack, data ownership, consistency model, external contracts, high-exit-cost vendors) from local reversible implementation details. Resolve local details yourself; bring open structural trade-offs to the user with a clear recommendation before committing dependent code.

## Make every boundary and layer pay rent

Draw boundaries around invariant enforcement, single-writer state ownership, independent deployment or change cadence, and failure containment. State each boundary's job in one causal sentence: what invariant it guards, what churn it isolates, or what blast radius it stops.

Audit layers ruthlessly. Pass-through wrappers, generic repositories over an ORM, and interfaces with a single foreseeable implementation add indirection without isolating anything — collapse them unless they protect a real ownership, testing, or compatibility seam. Split modules only when domain policy, infrastructure mechanics, and transport contracts repeatedly collide. Treat patterns (microservices, event buses, CQRS, plugin registries, hexagonal layers) as high-interest debt justified only when present forces pay their coordination, debugging, and consistency cost.

## Restrict extensibility to the credible change frontier

Place extension seams only where **both** likelihood of change and cost of late refactoring are high — active roadmap commitments, volatile third-party integrations, regulatory variance, or one-way data/protocol boundaries — and name the exact variance each seam absorbs.

Speculative futures are not requirements. Where change is unsubstantiated or cheap to refactor later with standard tools, write direct, cohesive code with low coupling rather than premature frameworks, config DSLs, or dead hooks.

## Validate choices against real paths and current facts

Compare only viable contenders against actual forces: capability fit, operational burden, failure behavior, team fluency, ecosystem health, and exit cost — then make a decisive recommendation rather than hiding behind neutral option tables.

Verify version limits, quotas, pricing, and semantics against current official documentation rather than model memory. When design success hinges on an unsettled technical assumption and execution is in scope, run a minimal throwaway spike or benchmark to settle it empirically before committing production structure. Stress-test proposed boundaries by tracing a representative write path, a partial downstream failure, and a credible requirement change end-to-end; shared mutable state and hidden distributed transactions surface under trace, not on box diagrams. Follow repository ADR conventions when durable documentation is warranted.

## Done when

The design, decision, or review resolves the architectural question directly; every boundary, layer, and technology choice traces to a concrete invariant, scenario, or constraint; critical technical claims are verified against source, official docs, or spike evidence (or flagged explicitly as unverified risks); accepted trade-offs and conditions that should trigger re-evaluation are stated plainly; and any user-owned fork required before implementation is surfaced cleanly.
