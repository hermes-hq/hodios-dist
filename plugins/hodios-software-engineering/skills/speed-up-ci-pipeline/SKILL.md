---
name: speed-up-ci-pipeline
description: Analyses a slow CI configuration and its job timings, then proposes caching, parallelism and test splitting with the minutes each change saves. Use when builds are slowing the team down.
license: CC0-1.0
arguments:
  - ci_config
  - timings
  - ci_system
argument-hint: <ci_config> [timings] [ci_system]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: devops
  source: https://hermes-ide.com/prompts/speed-up-ci-pipeline
  catalog: 2026.1002.1
---

# Speed up a CI pipeline

## Inputs

- `ci_config` (required): The pipeline configuration file or files.
- `timings` (optional): Recent job and step durations, ideally from several runs (p50 and worst case).
- `ci_system` (optional; one of: github-actions, gitlab-ci, circleci, other; default: github-actions): CI system the config is written for.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Developers wait on wall-clock time, and only the critical path through the job graph sets it. Shaving five minutes off a job that runs in parallel with a longer one saves nothing. Generic advice ("add caching", "use bigger runners") without the arithmetic leads teams to spend a week on changes that save seconds. Every proposal here must say how many minutes it removes from the critical path, and why.
</context>

<task>
Speed up this $ci_system pipeline:
$ci_config
Only if timings was provided: 
Observed timings:
$timings

1. Build the job graph from the config (stages, `needs` or dependencies, matrices, conditions) and find the critical path. If timings are missing, say so, estimate durations from typical step costs, label every number as an estimate, and tell the user which timing data would confirm it.
2. Look for savings in this order, because earlier items are cheaper and safer:
   - Skip work: path filters, affected-only builds in monorepos, cancelling superseded runs on the same branch, shallow clones.
   - Cache: dependency caches keyed on the lockfile hash and OS, build and compiler caches, container layer caches.
   - Restructure: replace serial stages with a dependency graph so independent jobs start together; move slow checks off the merge-blocking path only if the team accepts that.
   - Parallelise: shard tests by recorded timing, not by file count; size the shard count so setup time does not eat the gain.
   - Hardware: larger runners only where a job is CPU-bound and the cost is worth it.
3. For each change, estimate minutes saved on the critical path and on total compute, and show the arithmetic.
4. Flag hidden time sinks: retries that mask flaky tests, repeated dependency installs across jobs, artifacts uploaded and never used, Docker builds without cache.
</task>

<constraints>
- Cache keys must include the lockfile hash and the OS or image. Never share caches across trust boundaries, such as from fork pull requests into the main branch.
- Do not remove or weaken a required check to save time. If a check looks redundant, say so and let the team decide.
- Write config only in the syntax of $ci_system; if it is `other`, ask which system and stop before writing config.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
</constraints>

<output_format>
## Critical path
A table: job, duration, on the critical path (yes/no). Then the current wall-clock total.
## Changes
Numbered, ranked by critical-path minutes saved. Each: the change, minutes saved (critical path / total compute) with the arithmetic, effort (S/M/L), risk, and any cost change.
## Config changes
The edited config as a diff, for the top changes only.
## Expected result
Wall-clock before and after, and which numbers are estimates.
## Measure
How to confirm the gain over the next 20 runs.
</output_format>
