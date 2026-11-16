# Web Exploration (ego-lite Preferred)

Drive web dogfooding in a real rendered browser so visual hierarchy, density, interaction latency, and state transitions are observed firsthand rather than guessed from source.

## Browser driver priority and session safety

**Prefer `ego-lite` (`ego-browser`) whenever installed**, since it runs in a shared real Chromium environment with existing signed-in context and live human handoffs:

- Run `ego-browser skill` before the first browser call so `TaskSpace`, `Page`, selector, and `finish()` usage matches the installed runtime.
- Reuse one `TaskSpace` per dogfooding goal and navigate existing `Page` handles rather than spawning a tab per route; pass absolute file paths inside `ego-browser nodejs` scripts; batch predictable single-page actions + state waits (`waitForURL`, `waitForSelector`, `waitForFunction`) + trailing `snapshot()` into single calls.
- Protect shared profile state: leave user-owned tabs untouched, scope write probes to clearly named reversible test items, and preserve cookies, cache, and storage unless the user explicitly asks to clear state (after consulting `ego-browser`'s clearing-state rules).
- When unprovided credentials, SSO, 2FA, CAPTCHA, payment, or browser permission dialogs block progress, call `handOff()`, pause browser execution for that turn with clear instructions, and resume via `takeOverTaskSpace` once the user confirms.

**Fallback when `ego-lite` is unavailable**: In CI, remote sandboxes, or hosts without `ego-browser`, fall back cleanly to the best available live browser tool (`agent-browser`, a browser MCP server, or Playwright/Chromium automation). Record the fallback driver and any fidelity caveats (such as a clean unauthenticated profile or manual auth boundary) in the report header. Stop and report a browser blocker only when *no* live browser runtime can reach the target URL.

## Cold first-impression capture

On initial entry, wait for load and immediately capture both a viewport screenshot and a full-page screenshot plus a semantic snapshot **before** scrolling or clicking. Confirm the landed URL and frame first so an auth wall or error redirect is never critiqued as the workspace. Inspect the screenshot right away to lock in your cold 5-second hierarchy, density, and AI-slop read before familiarity dulls it.

## Single-pass DOM diagnostics to back visual judgment

Pair interactive walkthroughs (full-page snapshots when content extends below the fold, targeted screenshots at key transitions, and mobile `375x812` vs desktop `1440x900` checks) with a compact in-page JS evaluation on primary views to collect objective rendered metrics in one pass:

- **Token sprawl**: distinct `fontFamily` stacks, heading `fontSize`/`fontWeight` pairs, text/background colors, and `borderRadius` values across visible nodes.
- **Density and overflow**: `document.documentElement.scrollWidth > window.innerWidth` horizontal overflow, count of real domain records visible in the first viewport without scrolling, and share of visible words/height consumed by static banners, chrome, or happy-talk prose.
- **Hit-target and clipping defects**: interactive controls (`a, button, input, [role=button]`) whose `getBoundingClientRect()` falls below 24x24 CSS px (or 44x44pt on touch viewports), plus clipped overflow without accessible expansion.
- **Latency and silent failures**: serialized `performance.getEntriesByType("navigation")` metrics, in-page `fetch` checks when API behavior is suspect, and console/network error capture.

## Reproducibility and incremental logging

Re-trigger interactive failures once from a clean prior state to rule out transient misclicks, capturing `before -> action -> result` screenshots so any reader can verify the bug visually; static layout, density, and slop findings need one clear screenshot. Append confirmed findings and artifact paths to working notes immediately after each flow so long sessions never drop early evidence.
