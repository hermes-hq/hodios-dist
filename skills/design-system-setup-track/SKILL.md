---
name: design-system-setup-track
description: Sets up a first design system in gated steps - UI audit, tokens, the first ten components, usage docs, a pilot with one product team and a governance plan.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: design-systems
  source: https://hermes-ide.com/prompts/design-system-setup-track
  catalog: 2026.1004.0
---

# Set up a first design system

## Inputs

- [PRODUCTS] (required): The products the system must serve - platforms, tech stack, how many screens or apps, and anything already shared between them (a style guide, a UI kit, a component folder).
- [TEAM] (required): Who will build and run the system and how much of their time it gets, for example "one designer at 50%, two frontend engineers at 20%, no dedicated owner yet".
- [TOOLING] (optional): Design and code tools in use, for example "Figma, React with CSS modules, Storybook, a monorepo". Leave empty if undecided.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Takes a team from scattered UI to a first, small design system that one real product team uses. Most first systems fail in one of two ways: a large component library built in isolation that no product adopts, or a Figma kit that never reaches code. This track keeps the scope small (tokens plus about ten components), proves value with one pilot team before expanding, and treats the system as a product with users, a backlog and a release process.

Products: [PRODUCTS]
Team and capacity: [TEAM]
Only if [TOOLING] was provided: Tooling: [TOOLING]
Throughout: size every recommendation to the team's real capacity, and say what to drop if the capacity is too small. Ground decisions in what exists in the products (screens, code, usage counts the user supplies), not in a generic ideal component list. If tooling is undecided, recommend the lightest option that keeps design and code in step, and name it as an assumption. Never invent audit findings: when the user has not supplied screens, code or counts, give them a short collection task and wait for the results. Stop at the end of each step, summarise the decisions made, and wait for approval before the next step.

## Steps

Work through these steps in order. Do not skip a gate.

1. ui-audit (discover)
2. token-foundation (design)
3. first-components (design)
4. usage-documentation (design)
5. pilot (ship)
6. governance-plan (ship)

### Step 1: UI audit

Find what exists and where inconsistency costs most.

1. If inputs are missing, ask for screenshots of the 10 to 20 most-used screens, the main stylesheet or theme file, and the component folder listing, or give a one-hour collection task (screenshot every distinct button, input, modal and table; grep for hex colours and font sizes). Wait for results.
2. Inventory by element type (colours, type sizes, spacing, radii, shadows, buttons, inputs, modals, tables, alerts, navigation): distinct variants and which product uses each. Mark near-duplicates versus genuine variants.
3. Rank inconsistency by cost: frequency, number of teams rebuilding it, and bugs or accessibility issues caused (missing focus states, low contrast).
4. Note constraints: frameworks that cannot share code, theming or white-label needs, accessibility obligations, products being retired.

Output: inventory table, top five costs, constraints.

Stop. Ask the user to confirm the inventory and which products are in scope.

Save this step's result to `ui-audit`.

**Gate:** stop here and wait for the user's approval before step 2 (token-foundation).

### Step 2: Token foundation

Turn the audit into a small set of decisions everything else references.

1. Start with two tiers: primitives (palette, spacing, radii, type scale, shadows) and semantic tokens named by purpose (`color.text.default`, `color.border.focus`). Add component tokens later, only when needed.
2. Collapse near-duplicates into scales (spacing on a 4 or 8 px base, six to eight type sizes, two or three radii) and map each old value to its new token so migration is mechanical.
3. Keep semantic colours to tens, not hundreds, and list text-on-background pairs that must meet WCAG contrast (4.5:1 body, 3:1 large text and UI), marked "to verify" unless computed.
4. Decide naming, the source of truth and how tokens reach code (CSS custom properties, a theme object, platform files). Defer extra themes unless the pilot needs them.

Output: token tables, old-to-new mapping for the worst offenders, source-of-truth decision, contrast pairs.

Stop. Ask the user to approve the tokens before choosing components.

Save this step's result to `token-foundation`.

**Gate:** stop here and wait for the user's approval before step 3 (first-components).

### Step 3: The first ten components

Choose the components that pay back fastest.

1. Score candidates from the audit on frequency, number of duplicate implementations, and risk when built wrong (accessibility, data loss). Show the table.
2. Pick about ten by score (often button, inputs, select, checkbox and radio, link, icon, dialog, alert, card, a layout primitive, but follow the scores).
3. For each: variants now and deliberately left out, states, and the accessibility contract (keyboard, accessible name, focus management for overlays).
4. Build or adopt: wrapping an accessible headless library versus building, given capacity and framework, and the later cost of each.
5. Definition of done: design and code match, tokens only, documented, keyboard and screen-reader checked, visual regression snapshot, versioned release.

Output: scoring table, shortlist with scopes, build-or-adopt decision, definition of done.

Stop. Ask the user to approve the shortlist.

Save this step's result to `component-shortlist`.

**Gate:** stop here and wait for the user's approval before step 4 (usage-documentation).

### Step 4: Usage documentation

Write what people need to use a component correctly the first time.

1. Choose one source location for docs that design and code readers both use; other places link to it.
2. Page template per component: purpose and when not to use it, anatomy, variants and how to choose, states, content rules, accessibility notes, code usage, and do and don't examples from the real products.
3. A getting-started page: install, using tokens, getting help, reporting gaps.
4. Write the full page for the most used component as the worked example.

Output: docs location, template, getting-started outline, worked example.

Stop. Ask the user to approve before planning the pilot.

Save this step's result to `docs-plan`.

**Gate:** stop here and wait for the user's approval before step 5 (pilot).

### Step 5: Pilot with one product team

Prove the system in one real product before wider adoption.

1. Pick the pilot team with the user: building screens soon, willing, on the common stack, and not the hardest legacy code.
2. Agree scope (screens or flows), dates and who from the system team pairs with them.
3. Define success before starting: share of pilot screens built from the system, build time versus before, UI and accessibility defects, team rating. Capture baselines.
4. Set the feedback loop (channel, weekly check-in, gap log, response time) and release mechanics (versioning, changelog, upgrade path).
5. Write go or no-go criteria for a second team.

Output: pilot brief, success measures, feedback loop, rollout criteria.

Stop. Ask the user to confirm the pilot, or to report results if it has run.

Save this step's result to `pilot-plan`.

**Gate:** stop here and wait for the user's approval before step 6 (governance-plan).

### Step 6: Governance plan

Decide how the system keeps running once several teams depend on it.

1. Ownership: who decides, who maintains, protected time. If no one owns it, say plainly it will decay and propose the smallest viable arrangement.
2. Contribution: how a team proposes a component or variant, who reviews and how fast, and when a one-off stays local.
3. Versioning and deprecation: semantic versions, aliases for deprecated tokens and components, and how teams are told.
4. Adoption measures to review quarterly: code and design coverage, detached or overridden instances, open requests, satisfaction.
5. A first-year roadmap: next components, next teams, review dates.

Output: a governance one-pager and roadmap, ending with the three risks most likely to stall the system and an early warning sign for each.

Save this step's result to `governance-plan`.
