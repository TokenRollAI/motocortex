# Visual Sketch Craft, Diagrams, and Live Feedback Reference

Examples verified against Joplo `0.8.0` (including the Manus voice-input study, `agent-arch`, and the Global Voice IME sketch). Always run Joplo CLI commands from the demo project directory and consult installed `npx joplo skill` guides if package versions differ.

## Naming contrast: jargon vs user-legible titles

| Layer | Weak (jargon, slogan, or placeholder) | Strong (plain capability, mechanism, or situation) |
|---|---|---|
| Feature `name` | `AI Smart Voice Assistant` / `voice-ime-v2` / `Reimagining Input` | `Global voice input: dictate clean text into the active cursor` |
| Feature `goal` | `Add a floating capsule with streaming ASR` (locks one option) | `While writing a draft, dictate punctuated text into the current insertion point and decide when to send it` |
| Option `title` | `Option A` / `Default V1` | `Option A · Inline strip beside the caret` vs `Option B · Bottom floating capsule with rewrite preview` |
| Case `title` -> `expected` | `happy: Dictation works` / `edge_2: Cancel` | `Mis-speak in an existing draft and cancel` -> `Pressing Esc discards spoken words and leaves the original draft intact at the comma` |
| `flow()` / `chapter()` title | `Flow 1` / `Main scenario` | `Cancel mid-sentence without losing the existing draft` |
| Step caption | `Trigger state update` / `System callback` | `Press Esc: close the strip and keep the draft at the comma` |

## Visual stage patterns that explain implementation

- **Persistent workspace, state-driven transitions**: Model the host surface where the feature lives and drive transitions through state (`$.ui.*`) so viewers watch changes happen in place rather than reading static bullet cards.
- **Floating callouts and visible mechanics**: Use an `absolute`-positioned headline above the stage frame when highlighting a subtle invariant so window geometry never jumps; render invisible mechanics (active key state, progress/waveforms via CSS `@keyframes`, before-vs-after text cleanup) directly on screen so screenshots remain legible with subtitles hidden.
- **Keep player overlays and host styles clear**:
  - On the default `1280x800` desktop stage, leave breathing room at the top-left (step/completion badge) and bottom (~110–150px for keycap badges and spoken subtitles) so floating HUDs or prompts do not collide with player chrome.
  - Anchor inline caret popovers clear of wrapped lines (for instance above the caret with top padding on the editor), and scope custom CSS under your stage root class with explicit contrast on interactive triggers.

## Architecture and data-pipeline diagrams (`@joplo-app/plugin-diagram`)

Install the matching `@joplo-app/plugin-diagram` version, enable it in `joplo.config.ts` `plugins`, and run `npx joplo skill diagram` (syncing managed skill files via `npx joplo skill install .` when appropriate):

- **Choose the view that answers the review question**:
  - `<Diagram>`: Group services, workers, queues, and stores by domain (`Diagram.Group` + `Diagram.Node` with `kind` and `description`). Write forward request `Diagram.Edge` entries before return edges so automatic layout flows cleanly; prefix numbers in `label` manually (`1. Precheck quota`) when hop order matters, and add `async` on background/queue edges.
  - `<Sequence>`: Trace request, `reply`, `async` messages, and `Sequence.Block kind="par"` blocks when call ordering, prechecks, or post-response pipelines matter (message numbering is built into `Sequence`).
  - `<StateMachine>`: Bind `value={$.data.task.status}` to highlight lifecycle transitions (`idle -> validating -> running / awaiting_approval -> committed / failed`) alongside the pipeline.
- **Trace end-to-end data chains honestly**: Step through real or proposed hops (`producer -> validation -> transform/compute -> store -> consumer read-back`) using `trace(...)` (node chain when edges are unambiguous, edge IDs on parallel edges, message IDs in `Sequence`; pass `{ focus: false }` when inside a custom-camera `Canvas`) and `shot(...)` only when overriding default framing. Use `trace.fail(...)` to show failure or unknown-timeout reconciliation, labeling unbuilt guarantees as proposed rather than proven. Use standalone `work()` + `chapter()` when reviewing architecture alone without UI options.

## Verification and `feedback watch` operations

1. Check diagnostics and scenario IDs/durations (guide target is typically 5–12 steps, ~20–60s; >90s emits `SCENARIO_TOO_LONG` info):
   ```sh
   npx joplo check .
   npx joplo outline . --format json
   ```
   Read diagnostic counts directly because warnings still exit `0`.
2. Render storyboard sheets using qualified scenario IDs from `outline` (`<feature>.<option>.<scenario>` or `<work>.<scenario>`), then play the decisive flow once on the live board:
   ```sh
   npx joplo render . --scenario-id "<qualified-scenario-id>" --sheet --overwrite --out "rendered-check/<name>.png"
   ```
   If Chromium export tooling is absent, run `npx joplo setup export` when authorized or verify equivalent states in the live player and report the skipped export check.
3. Start the board and confirm the watcher is following before sharing the URL:
   ```sh
   npx joplo dev .                                           # prints the live URL; may attach to an existing hub and exit 0
   npx joplo feedback watch . --local --follow --json        # add --once only on hosts that resume on background exit
   ```
   Keep the owning board process alive (to run an isolated hub without touching another workspace's running board, set a private `JOPLO_HOME` *outside* the git checkout plus `--port <free-port>`; local review files still live in `<projectDir>/.joplo/reviews`). Because `--since` filters strictly (`createdAt > since`) and `--follow` attaches only to open rounds, check `npx joplo feedback list . --local --all --json` after any `--once` gap where a round may have approved/closed, replaying missed events via `npx joplo feedback watch . --local --session <id> --after <last-seq> --json` and deduplicating by `eventId`. For published Cloud Share reviews, poll `npx joplo feedback watch --share <share-id> --work <work-id> --json`.
