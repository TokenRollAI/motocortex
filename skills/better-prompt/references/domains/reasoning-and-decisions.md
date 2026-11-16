# Reasoning and Decisions

Covers math, formal logic, root-cause diagnosis, planning, trade-off analysis, and recommendations. Help the model frame the decision space and falsify weak conclusions — never script how its internal chain of thought should sound.

## Separate deliberation depth from visible auditability

Control internal search depth through the model's reasoning/thinking configuration rather than prompt slogans. In the prompt, specify what must be **externally auditable** in the response: governing constraints, explicit assumptions, key intermediate quantities or causal links, and independent sanity checks.

Route arithmetic, constraint solving, data aggregation, or factual lookups to code execution or retrieval tools whenever exactness matters, while avoiding pointless tool round-trips on self-contained logic. Prescribe step order only when compliance or proof validity demands a fixed protocol; otherwise state the invariants the final answer must satisfy and let the model decompose freely.

For decisions under uncertainty, separate verified facts, testable assumptions, and value preferences. Require a committed recommendation with explicit conditions under which an alternative wins, rather than symmetric pro/con lists that punt judgment back to the reader.

## Discriminating checks

Test multi-constraint interaction with plausible distractors, stability under wording/order perturbation, agreement between tool outputs and final prose, and honest exposure of underdetermined inputs instead of invented precision.
