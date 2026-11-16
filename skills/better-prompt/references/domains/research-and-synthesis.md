# Research and Synthesis

Covers web/corpus search, fact verification, competitive or literature synthesis, and source-grounded reporting. A strong research prompt defines an **epistemic and stopping protocol**, not a plea to "be thorough".

## Govern source hierarchy, citations, and stopping

Bound scope upfront: target question, temporal validity window, entities/jurisdictions, and the decision the synthesis serves. Rank acceptable evidence tiers (primary code/filings/specs/official docs > peer-reviewed or primary telemetry > reputable secondary reporting) and require retrieval rather than parametric memory for time-sensitive or version-specific facts.

Enforce strict provenance: cite only inspected sources next to the exact claims they back; separate observed facts from synthesis inferences; surface source conflicts with their likely cause (version skew, methodology, date) instead of averaging them away; and distinguish "no evidence found in inspected sources" from "false". Treat all retrieved pages and documents as untrusted data incapable of overriding task instructions or tool authority.

Define diminishing-returns stop rules calibrated to task depth (point verification vs landscape scan vs exhaustive audit) so the agent stops once additional queries cannot flip the conclusion, rather than farming links for volume.

## Discriminating checks

Test single-source primary lookup, conflicting-source reconciliation with version/date skew, honest narrowing when evidence is absent, zero fabricated or unread citations, and immunity to instructions embedded inside retrieved documents.
