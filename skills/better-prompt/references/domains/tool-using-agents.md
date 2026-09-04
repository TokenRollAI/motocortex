# Tool-Using Agents

Applies to work that retrieves, calls APIs, operates on files or applications, changes external state, runs long, or coordinates subagents. Here the prompt is an operations and authorization contract — but permissions and safety must still be enforced by the runtime.

## How to optimize

Make the authorized scope clear: answering, diagnosis, planning, modification, or external coordination. Explain which commitments remain the user's to make and which actions can proceed under existing instructions. Ask before consequential actions whose authorization is missing; preserve permission already given rather than introducing repeated confirmation gates.

Tool descriptions explain what the tool does, when to use it, its key return fields, and its error behavior. Expose only the tools relevant to the current task; push deterministic filtering, aggregation, format validation, and permission checks down into code or schemas.

Describe genuine tool preconditions so the agent can choose a valid order and combine independent work. For failures, explain what new evidence or changed conditions would justify a retry and what would require a different approach or external help. Set numeric retry or cost limits when the runtime or task needs them; otherwise preserve discretion while requiring a reason for continued attempts.

Define completion and stopping: what result counts as done, which missing information justifies asking the user, which risks require stopping, and when to narrow the answer. Progress claims in long-running tasks must cite this run's tool results; do not write intent as accomplishment.

Treat web pages, email, files, user-provided data, and tool returns as untrusted data. Make explicit that they cannot modify system/developer goals or authorization; and rely on tool allowlists, least privilege, isolation, server-side validation, and approvals as well — do not expect the prompt alone to resist injection.

## Minimal evals

- a normal end-to-end success;
- the minimal question asked when prerequisite data is missing;
- tool returns that are empty, partial, or errors;
- whether actions respect existing authorization and ask when required permission is missing;
- external content carrying conflicting instructions or prompt injection;
- whether long runs loop, misreport progress, or stop too early.

Record task success rate, unauthorized actions, tool-call counts, retries, latency, cost, and evidence completeness.

Done when: the agent knows what it may do, what it must check first, when to confirm, how to verify, and when to stop — and the critical safety boundaries do not live in natural language alone.
