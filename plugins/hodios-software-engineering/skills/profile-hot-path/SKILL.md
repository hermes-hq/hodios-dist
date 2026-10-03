---
name: profile-hot-path
description: Measures a slow operation, profiles where the time goes, and makes it faster one verified change at a time, with before-and-after numbers. Use when an endpoint, command or function is too slow.
license: CC0-1.0
arguments:
  - target
  - goal
  - environment
argument-hint: <target> [goal] [environment]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: performance
  source: https://hermes-ide.com/prompts/profile-hot-path
  catalog: 2026.1003.2
---

# Profile and speed up a hot path

## Inputs

- `target` (required): The slow operation (endpoint, command, function, job) and how to trigger it.
- `goal` (optional; default: as fast as reasonable changes allow; report the gain): The measurable target, for example "p95 under 200 ms at 50 requests per second".
- `environment` (optional): Where to measure and any limits (local machine, staging, production data size, no production access).

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Performance work without measurement is guessing, and guesses are usually wrong about where the time goes. The method is: make the slowness reproducible, measure it, profile it, change one thing, and measure again. A speedup that was not measured did not happen.
</context>

<task>
Speed up: $target
Goal: $goal.
Only if environment was provided: 
Environment and limits:
$environment

1. Define the scenario and the metric (latency percentiles, throughput, CPU time, memory or allocations) and the input size that matches real use.
2. Build a repeatable measurement: a benchmark, a load script or a timed command. Warm up first, run enough repetitions to see the variance, and record the baseline as a median with its spread.
3. Profile the scenario with a sampling profiler suited to the runtime (for example perf or a flame graph tool for native code, py-spy for Python, pprof for Go, async-profiler or JFR for the JVM, the built-in inspector for Node.js, dotnet-trace for .NET). Use what is installed, or ask before installing anything.
4. Classify where the time goes: CPU in our code, CPU in a library, waiting on I/O (database, network, disk), lock contention, or garbage collection. Name the top contributors with their share of the total.
5. Form one hypothesis, make one change, and re-run the measurement. Keep the change only if the gain is larger than the noise. Run the tests after each kept change.
6. Stop when the goal is met, or when the remaining contributors need a design change; then describe that change instead of making it.
</task>

<constraints>
- No optimisation without profile evidence pointing at it.
- One change per measurement, so every gain is attributable.
- Behaviour must stay identical; the tests must pass after every kept change.
- Skip micro-optimisations that make the code harder to read for a gain under about 5% unless the user asks for them.
- Report real measured numbers with the number of runs. Never estimate a speedup you did not measure.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
</constraints>

<output_format>
## Result
One line: metric before, after, number of runs, and whether the goal is met.
## Where the time went
Table: contributor, share of total before, share after.
## Changes
Numbered: the change — why the profile pointed there — measured effect.
## Not done
Bigger opportunities that need a design change or a decision, with the expected benefit stated as a hypothesis.
## How to reproduce
The exact commands to re-run the measurement.
</output_format>
