---
name: remove-dead-code
description: Finds unused code, flags, endpoints, jobs and dependencies, proves each dead with static and runtime evidence, and removes it or stages a reversible retirement. Use to shrink a codebase.
license: CC0-1.0
metadata:
  version: 1.1.0
  kind: prompt
  category: refactoring
  source: https://hermes-ide.com/prompts/remove-dead-code
  catalog: 2026.1004.0
---

# Remove dead code safely

## Inputs

- [SCOPE] (required): The directory, package or module to clean up.
- [PUBLIC_API] (optional; one of: yes, no, unknown; default: unknown): Whether code in scope is used outside this repository, for example a published library or a service other teams import.
- [EVIDENCE_SOURCES] (optional): Runtime evidence you have or can get, for example access logs, APM or metrics, production coverage, flag-evaluation data or job run history, with the time window each covers.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Dead code costs reading time, build time and false leads when debugging. But "no references found" is not proof of death: code is also reached through reflection, dependency injection, string lookups, routing tables, templates, serialization, plugins, scheduled jobs and callers in other repositories. Some code has no static references to find at all: HTTP endpoints called by other teams or old app versions, flags whose value lives in a flag service, scheduled jobs, config keys and message handlers. Whether they are used is a runtime fact, and "zero calls last week" is weak evidence when a caller runs at month end, at year end, or only on an old mobile release that is still installed. Removing live code is an outage; leaving dead code is only clutter. When in doubt, keep it, or turn it off reversibly first.
</context>

<task>
Find and remove dead code in [SCOPE]. Used outside this repository: [PUBLIC_API].
Only if [EVIDENCE_SOURCES] was provided: Runtime evidence available: [EVIDENCE_SOURCES]
1. **Find candidates:** unreferenced functions, classes, exports and files; branches that can never run; feature flags that are always on or always off; configuration nobody reads; dependencies nothing imports; and runtime-reachable paths that may be unused: HTTP or RPC endpoints, GraphQL fields, message consumers, scheduled jobs, and tables or columns written but never read. Use the language's tooling where it exists (compiler warnings, unused-export or unused-dependency tools) and text search.
2. **Prove each candidate dead.** Search the whole repository, not only the scope, for the name as a string as well as a symbol. Check dynamic dispatch and reflection, DI containers, routes, templates, config files, build scripts, cron and job definitions, serialization or ORM mappings, and tests.
3. **Classify:**
   - **dead**: no path reaches it, and it is not public API used elsewhere;
   - **likely dead**: no reference found, but it is reachable dynamically or by external callers;
   - **runtime-only**: no static reference, but whether it is used is a runtime fact (endpoints, jobs, flags in a flag service, message handlers, external callers);
   - **alive**: a reference was found.
4. Remove only **dead** items, in small commits grouped by kind, so each can be reverted alone. When a test exists only to exercise dead code, remove the test with it.
5. For **runtime-only** and **likely dead** items, grade the evidence on three rungs: static (no references, including string lookups); runtime (zero use in the evidence sources over a stated window, and whether that window covers monthly, quarterly and yearly cycles and the oldest supported client); ownership (the owning team or known consumers confirmed it is unused). Confidence is high with all three, medium with two, low with one. If no runtime evidence was given, say what to collect; never treat missing evidence as proof of no use.
6. Plan their retirement in stages, one change per stage so each reverts on its own: instrument (a log or metric on every entry to the path, tagged with caller identity) when evidence is missing; announce (deprecation notice, `Deprecation` or `Sunset` headers, changelog) for externally visible paths; soft-disable behind a kill switch, or return 410 Gone with a log line, keeping the code for a waiting period that covers the longest usage cycle; delete code, tests, config and flag definitions together, then now-unused dependencies in their own change; drop tables or columns only after the code that wrote them is gone and a backup exists. Order the items so that retiring one never breaks another that is still live.
7. Run the build, type checker, linter and tests after the removal.
</task>

<constraints>
- If [PUBLIC_API] is `yes` or `unknown`, treat exported or public symbols as **likely dead** at most, and do not remove them. Code that only runtime evidence can prove unused, such as endpoints, jobs and flags, needs a staged retirement, not a deletion.
- Only high-confidence items may be planned for deletion; medium items go to soft-disable; low items need more evidence. Nothing externally reachable is deleted without a soft-disable stage first.
- Name the exact evidence for each staged item: the query or log search, the window and the count. Do not invent numbers; write "missing" when evidence is missing.
- Write the staged retirement as a plan with change boundaries; do not make those changes unless asked.
- Never remove code just because it is old, commented as deprecated, or unused in tests only.
- Do not refactor or reformat code that stays.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Removed
A table: Item | Where | Evidence it was dead.
## Kept
A table: Item | Where | Why it was kept (likely dead or alive, and the reference found). Or "None".
## Staged retirement
A table: Item | Type | Static | Runtime (window, count) | Ownership | Confidence | Action (soft-disable / collect evidence / keep), then numbered stages with timing relative to start (week 0, week 4…), the signal that allows the next stage, and how to roll each stage back. Or "None".
## Verification
Build, type-check, lint and test commands with results.
</output_format>
