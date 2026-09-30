# Command-Line Interaction

A CLI is an interface for two audiences at once: a person at a terminal and a script in a pipeline. Design for the person first, and keep the script's contract stable. The same principles as a GUI apply: visible state, predictable actions, fast feedback, safe destructive operations, and helpful recovery.

## Output and streams

Write primary results and machine-readable data to stdout, and write diagnostics, progress, warnings, and errors to stderr, so people see messages while pipes receive only data. Detect whether each stream is a terminal separately. When a stream is not a terminal, drop animations, spinners, and interactive prompts from it.

An explicit request such as `--color=always` wins over detection, which only sets the default. By default, disable color when the stream is not a terminal, when the `NO_COLOR` environment variable is set to a non-empty value, when `TERM` is `dumb`, or when the user passes `--no-color`. Reserve warning and error colors for warnings and errors, and never rely on color alone to carry meaning.

Keep default output readable by people and easy to search with standard text tools: one record per line, no decorative borders, and no information hidden in grouping headers. Offer a machine-readable mode such as `--json`, and a plain mode when formatting would get in the way of parsing. Treat machine-readable output as a stable contract: adding fields is safe, while changing or removing existing ones breaks scripts. Git's plumbing commands and `git status --porcelain` illustrate this split: the human-oriented output may change between versions, while the script-oriented format is kept stable.

## Exit codes and errors

Exit with zero on success and non-zero on failure, and map distinct non-zero codes to the failure modes callers most need to distinguish. Validate input early and fail before doing partial work.

Write errors for people: what went wrong, in their terms, and how to fix it, such as the exact command or permission change. Do not print stack traces for expected failures; keep them behind a verbose or debug flag. When the intent is guessable, suggest the likely command, but do not run a state-changing correction automatically.

## Arguments, flags, and help

Prefer flags to positional arguments beyond one or two obvious ones, since flags can evolve without ambiguity or breaking callers. Give every flag a long form, and keep common names consistent with the ecosystem, such as `--help`, `--version`, `--verbose`, `--output`, `--force`, and `--dry-run`. Name commands with predictable verbs and resources with nouns.

Make `--help` show help regardless of other flags, and `-h` too unless the ecosystem already gives it another meaning, as in `ls -h` or `du -h`. Stop parsing options after `--`, so wrappers can pass help flags through to the commands they run. Lead help with examples of common use, list the most important flags first, and link to fuller documentation.

Resolve configuration in a predictable precedence, typically command-line flags, then environment variables, then project configuration, then user configuration, then system configuration, and document it.

## Prompts and dangerous operations

Prompt only when stdin is an interactive terminal, and give every prompt an equivalent flag or argument so the command can run unattended. With `--no-input` or in a non-interactive context, fail clearly when required input is missing and name the flag that supplies it. Do not echo secrets as they are typed.

Scale safeguards to consequences. A mild, easily recovered change needs no prompt. A moderate change, such as deleting a directory, deleting a remote resource, or a bulk modification that is hard to undo, usually warrants a confirmation and a `--dry-run` that describes what would change without doing it. A severe change, such as deleting an entire remote application, should be hard to confirm by accident, for example by typing the resource's name, with a matching flag such as `--confirm=<name>` for scripts. Watch for destructive effects hidden in innocent-looking changes, such as lowering a count that silently deletes resources, and treat them by their real severity. In non-interactive use, require an explicit `--force` or `--yes` for confirmed operations.

## Responsiveness and interruption

Print something within about 100 milliseconds, especially before network calls, so the tool does not look hung. Show a spinner or progress for longer work on terminals, and still surface logs and errors when something fails. Set timeouts on network operations.

On Ctrl-C, acknowledge immediately, clean up with a bounded timeout, and exit quickly; let a second Ctrl-C skip cleanup, and say so. Make operations idempotent where possible and assume a previous run may have stopped midway, so rerunning the same command after a transient failure continues or converges instead of corrupting state.
