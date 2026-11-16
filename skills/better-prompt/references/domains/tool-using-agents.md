# Tool-Using Agents

Covers workflows that query external state, mutate files/databases/APIs, orchestrate subagents, or run multi-step loops. Here the prompt defines **operational judgment and delegation scope**, while hard safety and access control stay enforced in runtime code.

## Bound authority, preconditions, and loop termination

Draw an unambiguous line between autonomous actions (reads, reversible local work, actions inside already-granted scope) and commitments requiring fresh user approval (irreversible mutations, external comms, spend, permission changes, scope expansion). Reuse granted authorization instead of nagging on every step.

Keep toolsets lean and push deterministic filtering, schema validation, pagination math, and permission gates into tool implementations. Document each tool's preconditions, side effects, idempotency, and error semantics so the agent can parallelize independent calls and decide intelligently between retry (transient fault + safe idempotency), pivot (new hypothesis needed), or escalation (missing authority or external blocker).

Anchor progress reporting to observed tool outputs from the current run — never narrate planned actions as completed state. Fence untrusted external content (web pages, emails, issues, tool payloads) explicitly so injected directives cannot hijack goals or trigger side-effecting tools.

## Discriminating checks

Test clean end-to-end execution with parallelizable calls, surgical escalation when authority or critical input is missing, graceful recovery on empty/partial/failing tool responses, prompt-injection resistance across tool outputs, and loop termination without thrashing or premature exit.
