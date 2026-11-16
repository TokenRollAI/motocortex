# Command-Line Interaction

A CLI serves two callers simultaneously: an interactive human at a TTY and an unattended script in a pipeline. Optimize ergonomics for the human while keeping the machine contract additive and unbreakable.

## Stream separation, TTY detection, and output stability

Emit primary payloads and structured output exclusively on `stdout`; route progress, warnings, prompts, and diagnostics to `stderr` so pipelines stay clean. Check TTY status independently on `stdin`, `stdout`, and `stderr`: suppress spinners, ANSI cursor control, and interactive prompts whenever the relevant stream is non-TTY.

Honor explicit flags (`--color=always|never`) over environment defaults; otherwise disable ANSI color when non-TTY, `NO_COLOR` is non-empty, or `TERM=dumb`, and pair color with text/symbol prefixes. Keep default human output line-oriented and `grep`/`awk`-friendly without decorative box borders, and expose `--json` (or `--plain`) as a backwards-compatible contract where fields may be added but never silently renamed or dropped.

## Exit codes, flags, and error recovery

Fail fast on invalid inputs before mutating state, mapping distinct non-zero exit codes to actionable failure classes (usage error vs auth vs conflict vs transient network). Write human-readable errors on `stderr` naming what failed and the exact flag, command, or permission change that fixes it; gate raw stack traces behind `--debug` or `--verbose`, and never auto-execute guessed state-changing typos.

Prefer explicit `--long-flags` over positional arguments past one or two obvious targets, honor `--` to terminate option parsing, make `--help` side-effect-free with common usage examples at the top, and document config precedence (`flags > env > project config > user config > defaults`).

## Non-interactive safety, liveness, and signal handling

Prompt only when `stdin` is a TTY, providing a flag equivalent for every prompt; in non-TTY or `--no-input` runs, exit immediately naming the missing flag, and never echo secrets. Scale destructive safeguards to blast radius: silent + undoable for trivial local edits, `--dry-run` + confirmation (`--yes`/`--force` in scripts) for moderate mutations, and resource-name confirmation (`--confirm=<name>`) for irreversible remote destruction — including implicit destruction such as scaling replicas or retention to zero.

Acknowledge slow network/disk commands within ~100ms on TTY `stderr`, bound all I/O with timeouts, handle first `SIGINT` with bounded cleanup and second `SIGINT` with immediate exit, and design mutations idempotently so re-running an interrupted command converges safely.
