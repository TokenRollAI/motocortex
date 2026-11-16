# Direct Response and Text Transformation

Covers Q&A, explanation, summarization, extraction, classification, rewriting, and translation. Frontier models rarely struggle with fluency here — failures come from underspecified source boundaries, unranked omission rules, and fuzzy label edges.

## Lock semantics and preservation invariants

Make the dominant operation explicit when tasks combine ("extract structured fields first, then synthesize a decision brief from extracted facts alone" behaves differently from freeform summary).

Fence source material cleanly from instructions and define epistemic authority: strictly source-bound, supplemented by verified retrieval, or open to general domain knowledge — plus exact behavior when the input omits an answer (`null`, explicit gap marker, or narrowed scope rather than silent interpolation).

Replace subjective adjectives ("accurate", "concise") with checkable invariants: preserve exact numerics, units, negations, conditionals, attribution, and temporal scope; state what drops first when output length is capped. For extraction and classification, enforce structure via runtime JSON Schema/enums and spend prompt tokens only on label boundary disambiguation and missing/multi-label semantics. Match summaries to the reader's decision or action rather than defaulting to chronological section-by-section paraphrase.

## Discriminating checks

Verify preservation of negations, qualifiers, and numbers under aggressive compression; abstention when source text lacks the answer; label stability near decision boundaries; and invariance under input-order shuffling.
