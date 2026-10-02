<context>
Some code has no static references to find: HTTP endpoints called by other teams' services or old app versions, feature flags whose value lives in a flag service, scheduled jobs, config keys and message handlers. Whether they are used is a runtime fact. "Zero calls last week" is weak evidence when a caller runs at month end, at year end, or only on an old mobile release that is still installed. Safe retirement collects runtime evidence over a window that covers those cycles, turns the path off in a way that is instantly reversible, waits, and only then deletes.
</context>

<task>
Plan the retirement of unused code paths in:
[SCOPE]

If no runtime evidence is listed, say what to collect and plan the instrumentation step first; do not treat the absence of evidence as evidence of no use.

1. **List candidates** by type: HTTP or RPC endpoints, GraphQL fields, message consumers, scheduled jobs, feature flags (fully on, fully off, or unchanged for a long time), config keys, database tables or columns written but never read, modules, and dependencies. Use the repository where available to find each one's definition and static references.
2. **Grade the evidence** for each candidate on three rungs:
   - static: no references in this repository, including string lookups, routes, config and templates;
   - runtime: zero use in the evidence sources over a stated window, and whether that window covers monthly, quarterly and yearly cycles and the oldest supported client version;
   - ownership: the owning team or known external consumers confirmed it is unused, or nobody is known to own it.
   Assign confidence: high (all three), medium (two), low (one). Only high-confidence items go to deletion; medium items go to soft-disable; low items need more evidence.
3. **Plan the stages** for each item, with a commit or change per stage so each is reverted on its own:
   - instrument: add a log or metric on every entry to the path, tagged with caller identity, if evidence is missing;
   - announce: deprecation notice, `Deprecation`/`Sunset` headers or a changelog entry for externally visible paths;
   - soft-disable: turn off behind a kill switch or flag, or return 410 Gone with a log line, keeping the code; set a waiting period that covers the longest usage cycle;
   - delete: remove code, tests, config and flag definitions together; remove now-unused dependencies last, in their own commit;
   - schema: drop columns or tables only after the code that wrote them is gone and a backup or export exists.
4. Order the items so that removing one never breaks another that is still live.
</task>

<constraints>
- Never recommend deleting anything with low confidence, or anything externally reachable without a soft-disable stage first.
- Name the exact evidence for each item: the query or log search, the window and the count. Do not invent numbers; if evidence is missing, the cell says "missing".
- This is a plan with commit boundaries. Do not write the deletions themselves unless asked.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
</constraints>

<output_format>
## Candidates
Table: Item | Type | Static | Runtime (window, count) | Ownership | Confidence | Action (delete / soft-disable / collect evidence / keep).
## Evidence gaps
For each item without enough evidence: what to instrument or query, and how long to wait.
## Staged plan
Numbered stages with dates relative to start (week 0, week 4…), each listing the commits or changes and the signal that allows the next stage.
## Rollback
How to restore each stage: flag flip, revert commit, or restore from backup, and how fast.
</output_format>
