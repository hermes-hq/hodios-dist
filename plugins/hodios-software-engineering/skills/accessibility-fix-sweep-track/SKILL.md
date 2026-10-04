---
name: accessibility-fix-sweep-track
description: Fixes accessibility issues across a web app with a scan, keyboard and accessibility-tree checks, small fixes, a re-scan and a list for human testing. Use to clear accessibility debt in a sprint.
license: CC0-1.0
arguments:
  - app_url_or_routes
  - scan_command
  - standard
argument-hint: <app_url_or_routes> [scan_command] [standard]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: accessibility
  source: https://hermes-ide.com/prompts/accessibility-fix-sweep-track
  catalog: 2026.1004.0
---

# Accessibility fix sweep for a web app

## Inputs

- `app_url_or_routes` (required): The local URL of the running app and the routes or user flows to cover, most important first, for example "http://localhost:3000 - sign up, checkout, account settings".
- `scan_command` (optional): An existing accessibility scan command, for example an axe or pa11y script. Leave empty to use what the project already has or a local axe-based run.
- `standard` (optional; default: WCAG 2.2 AA): The conformance target to measure against.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Fixes accessibility problems in this web app against $standard, at the source. Automated scanners find only part of the problems, mostly missing names, contrast and invalid ARIA; keyboard traps, confusing focus order and unannounced updates need a person or an agent driving the page. This track combines both, fixes issues in the shared components they come from, and ends with an honest list of what still needs testing with real assistive technology.

Rules for every step:
- Report only what a scan or a check actually showed, with the route, element and how it was found.
- Fix at the source: the shared component, design token or layout, not one instance at a time.
- Prefer native HTML elements and attributes over ARIA. Add ARIA only where no native element fits, and then follow the ARIA Authoring Practices pattern for that widget.
- Never claim the app conforms to $standard. Automated and agent checks support a conformance review; they do not replace one.
- Do not silence scanner rules, add `aria-hidden` to hide failures, or exclude routes to improve the numbers.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
- Fix the behaviour, not the test. Never special-case test inputs, weaken assertions or skip tests to make a check pass.
- If a test looks wrong, explain why and ask before changing it.

## Steps

Work through these steps in order. Do not skip a gate.

1. scan (discover)
2. manual-checks (verify)
3. fix (build)
4. rescan-report (verify)

### Step 1: Automated scan

<targets>
$app_url_or_routes
</targets>

1. Start the app locally the way the project documents. If it cannot be started, or a flow needs credentials or test data you do not have, list what is missing and stop.
2. Run $scan_command if given; otherwise use the project's existing accessibility tests, or an axe-based scan of each route through a headless browser, including states reached by interaction (open menus, dialogs, validation errors, empty and loading states).
3. Map each violation to its source: the component or template file, the stylesheet or token behind a contrast failure. Group identical violations that share a source.
4. Record each group with the success criterion it maps to, its impact (blocks a task, makes it harder, cosmetic), and the routes affected.

Write the artifact: How the scan ran, Violations by source (Source | Rule | Criterion | Impact | Instances | Routes), Routes not reached and why. Continue to step 2.

Save this step's result to `a11y-sweep/01-scan.md`.

### Step 2: Keyboard and accessibility-tree checks, then a fix plan

For each key flow, in order of importance:

1. Keyboard only: can every control be reached with Tab and operated with Enter, Space and arrows as its role expects; is focus always visible; does focus order follow the visual order; can every dialog, menu and popover be closed with Escape and does focus return to where it was; is there any trap; is there a skip link or landmark navigation.
2. Accessibility tree (through the browser's accessibility snapshot or devtools protocol): every control has a meaningful name, the right role and its current state (expanded, selected, checked, invalid); headings form a sensible outline; form fields are tied to labels and errors; status messages and async updates are announced through a live region or focus move.
3. Visual: reflow at 320 CSS pixels wide and 400% zoom without horizontal scrolling for text, text spacing overrides, non-text contrast of focus rings and control borders, nothing conveyed by colour alone, motion respecting reduced-motion preferences, target sizes.
4. Merge these findings with step 1 by source. Rank by impact on completing the flow, then by number of users and routes affected.

Write the artifact: Manual findings (Flow | Step | Issue | Criterion | Source | How found), Fix plan (Source | Fix | Issues resolved | Regression test), Out of scope (content issues such as captions or alt text that need authors, third-party widgets). Stop and wait for approval.

Save this step's result to `a11y-sweep/02-findings-and-plan.md`.

**Gate:** stop here and wait for the user's approval before step 3 (fix).

### Step 3: Fix in small commits

1. Fix one source per change, following the approved plan: native elements in place of clickable divs, labels and names, focus management in dialogs and route changes, visible focus styles, live regions for async status, contrast through design tokens rather than one-off colours.
2. After each fix, re-check the affected flow with the keyboard and the accessibility snapshot, and rerun the scan for the affected routes.
3. Add a regression test where the project has a place for it: an axe assertion in component or end-to-end tests, a keyboard interaction test for the widget, or a contrast check on tokens.
4. Keep each commit to one issue type so a reviewer can verify it. Do not mix in unrelated refactors or visual redesign.
5. Run the project's existing tests and linters after each fix.

Continue to step 4.

### Step 4: Re-scan and report

1. Rerun the full scan from step 1 and the keyboard checks from step 2 on every flow.
2. Write the report:

#### Result
Violations before and after by impact, from real runs, and flows that can now be completed by keyboard.

#### Fixed
Table: Source | Issue | Criterion | Fix | Regression test.

#### Still open
Table: Issue | Why not fixed (needs content, design decision, third party, out of scope) | Suggested owner.

#### Needs human testing
Specific checks with real assistive technology that this sweep could not settle: screen readers on the platforms the users have (for example NVDA or JAWS with a Windows browser, VoiceOver on macOS and iOS, TalkBack on Android), voice control, switch access, and checks with disabled users. Name the flows and what to listen or look for.

#### Checks run
Commands and results.

Save this step's result to `a11y-sweep/04-report.md`.
