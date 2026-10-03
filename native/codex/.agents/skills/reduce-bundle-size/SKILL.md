---
name: reduce-bundle-size
description: Measures a web app's JavaScript bundles, finds the largest avoidable contributors, and shrinks them with verified changes ranked by bytes saved. Use when page load is slow or a size budget is blown.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: performance
  source: https://hermes-ide.com/prompts/reduce-bundle-size
  catalog: 2026.1003.2
---

# Reduce JavaScript bundle size

## Inputs

- [TARGET] (required): The app, page or entry point to shrink.
- [BUDGET] (optional; default: as small as the changes below allow; report the savings): The size budget, for example "initial JavaScript under 170 KB compressed".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
JavaScript is the most expensive byte on the web: it has to be downloaded, parsed and executed before the page responds. Most bundles carry avoidable weight: whole libraries imported for one function, duplicate versions, code for routes the user has not visited, and polyfills for browsers the app does not support. Savings only count when measured on the production build, compressed.
</context>

<task>
Reduce the bundle size of: [TARGET]
Budget: [BUDGET].

1. Identify the bundler and build. Produce a production build and record the baseline: the initial JavaScript loaded by the target page and the total, both compressed (gzip or brotli, whichever the server uses).
2. Generate a bundle analysis with the tool that fits the bundler (for example a bundle visualizer plugin, the bundler's stats output, or source-map-explorer).
3. List the largest contributors and classify each: needed on first load, needed only later or on another route, duplicated, imported wholesale but used partly, polyfill or dead code that was not tree-shaken, or a large asset inlined into JavaScript.
4. Fix in order of bytes saved per effort: lazy-load routes and heavy components with dynamic imports, switch to per-function or ESM imports, deduplicate versions, drop polyfills outside the supported browser list, and mark side-effect-free packages so they tree-shake.
5. Rebuild after each change and record the size difference. Run the tests and check that the affected pages still work.
</task>

<constraints>
- Do not remove features or change behaviour to save bytes.
- Replacing a dependency with another is a proposal, not a change, unless the swap is trivial and fully covered by tests.
- Report compressed sizes from real builds. Never estimate savings you did not build.
- Keep lazy-loading changes from causing layout shift or an empty screen; add a loading state where one is needed.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
</constraints>

<output_format>
## Result
One line: initial JavaScript before and after (compressed), total before and after, and whether the budget is met.
## Biggest contributors
Table: module or package, compressed size, classification.
## Changes made
Numbered: change — bytes saved (compressed) — verification.
## Proposals not applied
Bullets: proposal — expected saving as a hypothesis — trade-off.
## How to measure again
The exact commands.
</output_format>
