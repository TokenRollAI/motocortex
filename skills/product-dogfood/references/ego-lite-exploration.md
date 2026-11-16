# Web Exploration with ego-lite

Use this guide when dogfooding a web application so live exploration follows `ego-lite` (`ego-browser`) idioms, preserves the user's browser environment, and gathers sharp visual and runtime evidence without Playwright or headless browser tooling.

## Align with the installed ego-lite runtime

Before issuing the first browser command in a session, run `ego-browser skill` and follow its current TaskSpace, Page, selector, and lifecycle rules. Keep one TaskSpace for the entire dogfooding goal, reuse existing Pages with navigation rather than spawning a tab per URL, use absolute file paths inside `ego-browser nodejs` scripts, and close out completed browser work with `finish()` according to the user's expectations.

Keep Playwright, Puppeteer, and standalone headless browsers out of the workflow even when installed on the machine. If `ego-browser` is missing, disconnected, or unable to reach the target URL, report that exact operational blocker and stop browser claims there rather than falling back to another browser runner or inferring UI behavior from source files.

## Protect shared sessions and user control

`ego-lite` runs in a real Chromium environment designed for human and agent collaboration, often carrying the user's active logins and personal tabs. Leave user-created tabs untouched, create clearly named reversible test items when exercising write flows, and avoid destructive actions against real workspace data unless scoped to an isolated test project or authorized by the user.

Preserve cookies, cache, and local storage by default. Consult `ego-browser`'s clearing-state guidance and get explicit user confirmation before clearing any browser state, since clears can affect the wider profile.

When authentication without provided credentials, SSO, 2FA, CAPTCHA, payment confirmation, or a browser permission dialog blocks a flow, call `handOff()`, end the browser script for that turn, and tell the user what to complete in the browser window. Resume the same TaskSpace once they confirm instead of guessing credentials or routing around verification gates.

## Capture unfiltered first impressions first

Navigate to the entry URL, wait for initial load, and immediately take both a viewport screenshot and a full-page screenshot (saved to an absolute evidence directory) plus a semantic `snapshot()` before clicking or scrolling. Check the current URL and screenshot first so you do not mistake an unauthenticated redirect or login wall for the main product interface.

Read that initial screenshot with an image-viewing tool right away and write down your five-second visual hierarchy, density, and AI-slop read while your eyes are still fresh; familiarity after ten minutes of testing dulls first-time confusion.

## Pair semantic walkthroughs with objective DOM checks

Use `page.snapshot()` (and `scope: "full_page"` when content extends below the fold) together with semantic refs or role/text locators to drive tasks efficiently, waiting on observable URL, selector, or function conditions rather than arbitrary sleeps. Capture screenshots whenever a layout, state transition, density problem, or error matters to the report.

Supplement visual inspection with compact `page.evaluate()` probes on key screens to ground UI and density feedback in rendered facts rather than impressions alone:

- **Rendered design tokens**: Collect distinct `fontFamily`, heading `fontSize` and `fontWeight` pairs, text and background colors, and `borderRadius` values across visible elements to spot ad-hoc token sprawl or flat hierarchy.
- **Viewport efficiency and overflow**: Compare `document.documentElement.scrollWidth` against `window.innerWidth` for unintended horizontal scroll, count how many real domain records appear above the fold on operational views without scrolling, and measure how much of the first viewport is consumed by static banners, chrome, or happy-talk prose.
- **Target ergonomics**: Measure `getBoundingClientRect()` on visible links, buttons, and inputs to catch cramped hit targets (below 24x24 CSS pixels on desktop/web minimums or 44x44 points on touch viewports) and overlapping or clipped labels.
- **Perceived responsiveness**: Read `performance.getEntriesByType("navigation")` (serialized inside the page) and time key interactive transitions when sluggishness is noticeable.

Test responsive behavior on web products meant for multiple screen sizes by resizing or checking mobile (`375x812`) alongside desktop (`1440x900`) viewports, restoring the viewport afterward. When silent failures occur, check network behavior with `page.fetch()` where appropriate or enable console observation carefully during debugging as documented by `ego-browser skill`.

## Verify reproducibility and log incrementally

When an interactive flow breaks, misbehaves, or loses state, repeat the trigger once from a clean prior state to confirm reproducibility, saving before, action, and result screenshots so a reader can see the failure sequence without re-running the browser. Static visual, density, and copy issues need only one clear screenshot.

Write confirmed findings and their absolute screenshot paths into your working notes immediately after each flow so interrupted or multi-flow runs retain every piece of evidence.
