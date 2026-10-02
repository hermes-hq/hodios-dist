---
name: find-memory-leak
description: Finds a memory leak from heap snapshots, memory metrics and code, naming the retaining path and the minimal fix with a regression check. Use when memory grows until a process is killed or restarted.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: performance
  source: https://hermes-ide.com/prompts/find-memory-leak
  catalog: 2026.1002.2
---

# Find a memory leak

## Inputs

- [SYMPTOMS] (required): What you observe - memory over time, restarts or OOM kills, when it started, load pattern, recent changes, and suspect code if any.
- [HEAP_DATA] (optional): Heap snapshot comparison, allocation profile, retainer paths, GC logs or pprof output.
- [RUNTIME] (optional): Runtime and version, e.g. "node 22", "jvm 21", "go 1.23", "python 3.12", "browser (react app)".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Not every rising memory graph is a leak. A cache warming up, a heap the runtime has not shrunk, fragmentation, or off-heap buffers all look similar from a dashboard. A real leak is memory that stays reachable after the work that needed it is done, and it is proven by a retaining path: the chain of references from a GC root to the objects that keep accumulating. Fixes made without that path tend to move the leak rather than remove it.
</context>

<task>
Find the leakOnly if [RUNTIME] was provided:  in this [RUNTIME] process.
Symptoms:
[SYMPTOMS]
Only if [HEAP_DATA] was provided: 
Heap and profiling data:
[HEAP_DATA]

1. If the runtime is unknown and matters for the next step, ask for it and stop.
2. Classify the growth first: a leak (the floor after each garbage collection keeps rising under steady load), unbounded but intended growth (a cache without limits), runtime heap behaviour, fragmentation, or off-heap or native memory (RSS grows while the managed heap is flat). Say which evidence supports the classification.
3. If heap data is missing or insufficient, give the exact capture steps for this runtime: two or three snapshots taken after a forced GC under the same load, minutes apart, compared by retained size and object count. Stop there with hypotheses ranked by likelihood.
4. With heap data, find the object types whose count grows between snapshots, and follow their retainers back to a GC root. Write that chain as the retaining path.
5. Match the path to code. Typical causes: maps or caches keyed by request or user without eviction, event listeners and subscriptions never removed, timers and intervals never cleared, closures capturing large objects, static or global registries, thread-locals in pooled threads, goroutines blocked forever on channels or missing context cancellation, detached DOM nodes held by JavaScript.
6. Propose the smallest fix that breaks the retaining path, and a regression check that fails before the fix.
</task>

<constraints>
- Do not claim a cause without evidence from the data or the code. Mark each hypothesis with what would confirm or rule it out.
- Do not recommend raising the memory limit or scheduled restarts as the fix. You may mention them as a stop-gap, labelled as such.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Verdict
Leak, not a leak, or not yet determined, with one sentence of evidence.
## Retaining path
GC root → … → leaking objects, or "Not yet established".
## Evidence
Bullets citing snapshot numbers, metrics or code locations.
## Fix
A diff and one sentence on why it breaks the path.
## Regression check
A test or soak check that repeats the operation many times and asserts memory or object count stays bounded.
## Next captures
What to capture next if anything is unconfirmed, or "None".
</output_format>
