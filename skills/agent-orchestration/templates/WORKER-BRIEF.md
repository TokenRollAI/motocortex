# Worker Brief Template

Keep each brief compact and proportional to the task (investigation vs implementation). Supply shared context once in a shared file when fanning out to multiple workers, and put only slice-specific ownership, contracts, and checks in the per-worker brief.

<worker-brief-template>
# Task <task-id>: <one-line deliverable>

## User intent and observable outcome

- Surface and actor: <exact product view, CLI command, API endpoint, caller path, or audit target>
- Expected outcome: <action -> observable end-to-end result (including write -> read-back) or specific research question to answer>
- Intent source and rules: <verbatim user constraints, non-goals, reviewed demo reference if already settled, and any reversible working assumption>

## Verified context and ownership

- Workspace: `<absolute cwd or worktree path>` on branch `<branch>` (base `<commit/branch>`)
- Mode and owned paths: `<read-only | write limited to exact files/directories; commit/merge rules>`
- Off-limits / neighboring work: `<shared contracts, sibling worker files, or generated outputs not to hand-edit>`
- Verified facts vs open investigation: <facts Coordinator confirmed with file:line pointers, separated from what Worker still needs to trace>

## Contracts and autonomy bounds

- Upstream / downstream interfaces: <exact procedure names, payload/return shapes, or exported type paths consumers rely on>
- Authorized mechanical wiring: <specific route registration, exports, or codegen within scope; include migrations or shared-config edits only when explicitly authorized>
- Escalate to Coordinator (`NEEDS_DECISION` / `BLOCKED`): <conflicting instructions, missing inputs, cross-owner edits, scope expansion, or acceptance threshold changes — never guess or ask the user directly>

## Functional check and stop condition

- Required proof: <minimal real entry-point walkthrough, write -> read-back check, reproducer, or source-backed audit evidence that proves this slice>
- Shared-resource limits: <shared DBs, ports, or test suites in use by sibling workers, or `None`>
- Stop when: <exact condition where the deliverable and its functional proof are complete — without speculative defensive wrappers or unrequested full-repo test churn>

## Reporting

- Return channel: <`hc send <literal-coordinator-address> "<summary>"`, subagent reply, mail, or `.done` / `.blocked` signal>
- Agreed report path: `<writable file path inspected by Coordinator if push delivery fails>`
</worker-brief-template>
