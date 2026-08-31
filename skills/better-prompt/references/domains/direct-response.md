# Direct Response and Text Transformation

Applies to Q&A, explanation, summarization, extraction, classification, rewriting, and translation. The dominant risk here is not that the model cannot write — it is that the answer's scope, factual boundaries, preservation rules, and output contract were never stated.

## Determine the task first

- Q&A / explanation: what problem is the user solving, for whom, at what depth?
- Summarization: what must be covered, what may be dropped, is the source text the only ground?
- Extraction / classification: how are fields or labels defined, how are missing and ambiguous values represented?
- Rewriting / translation: which facts, structure, terminology, tone, and length must be preserved?

When one prompt mixes these actions, make the main task and its priority explicit. "Extract first, then summarize" and "summarize, extracting along the way" are not the same contract.

## How to optimize

Separate input from instructions and state the source boundary. For grounded output, say which materials alone may be used, when common knowledge or external retrieval is allowed, and how to narrow the answer when evidence falls short.

Replace vague style words with concrete preservation rules. "Preserve all numbers, proper nouns, and causal relations" is more checkable than "rewrite accurately". For short answers, state what must survive, not merely "be concise".

For classification and extraction, prefer API schemas or enums. The prompt explains field semantics, ambiguity, and missing values; the schema owns the syntax. Add minimal examples only when label boundaries fail repeatedly.

Do not default summaries to section-by-section recitation. Choose a coverage, decision, action, or compression summary by the user's purpose, and give length and omission priorities.

## Minimal evals

- does a typical input complete the core task directly;
- does the model avoid guessing when a field is missing or the source has no answer;
- are numbers, proper nouns, qualifiers, and negations preserved;
- are label boundaries, format, and length stable;
- does paraphrasing or input reordering cause intent drift.

Done when: the model knows what to answer, what it may rely on, what it must preserve, and how to behave when information falls short.
