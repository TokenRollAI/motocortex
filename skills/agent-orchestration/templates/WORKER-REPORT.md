# Worker Report Template

Use `DONE` when the assigned deliverable and its agreed evidence are complete. Use `NEEDS_DECISION` or `BLOCKED` as soon as a missing input, contract conflict, or cross-boundary fork is found — include only the sections needed to unblock the ruling immediately.

<worker-report-template>
# Worker Report: <task-id> [<DONE | NEEDS_DECISION | BLOCKED>]

## Outcome or decision fork

- If `DONE`: <concise statement of delivered behavior or audit findings, plus any authorized mechanical wiring>
- If `NEEDS_DECISION` | `BLOCKED`: <missing input or exact conflict | affected work | concrete reproducer/options + recommended choice when applicable | orthogonal work continuing meanwhile>

## Files and contract handoff (when `DONE` or partially staged)

- Workspace / state: `<cwd or worktree>` (`<branch / commit / clean read-only>`)
- Touched files: `<comma-separated paths or none>`
- Consumer contract: `<procedure names, payload/return shapes, or type paths ready for downstream slices, or none>`

## Functional verification

- Observed proof: <commands, live UI/CLI checks, write -> read-back results, or cited `file:line` evidence>
- Baseline / unrun notes: <pre-existing unrelated failures or environment-gated checks separated from this slice, or `None`>
</worker-report-template>
