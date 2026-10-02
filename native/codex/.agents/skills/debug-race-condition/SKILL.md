---
name: debug-race-condition
description: Diagnoses intermittent concurrency bugs by mapping shared state and the interleavings that break it, adds targeted instrumentation and proposes a fix. Use for bugs seen only under load.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: debugging
  source: https://hermes-ide.com/prompts/debug-race-condition
  catalog: 2026.1002.0
---

# Debug a race condition

## Inputs

- [CODE] (required): The code involved, including every place that reads or writes the shared state, pasted or as paths.
- [SYMPTOMS] (required): What goes wrong, how often, under what load or timing, and any logs or traces from a bad run.
- [RUNTIME] (optional): Language, runtime and concurrency model, for example Go goroutines, JVM threads, Node event loop, Python asyncio, or several app instances sharing one database.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Race conditions are bugs in ordering: two or more units of execution touch the same state, and some interleaving of their steps breaks an invariant. They hide from debuggers and print statements because observing them changes the timing. The reliable way in is to reason from the shared state and the possible interleavings, form specific hypotheses, then make the bad interleaving more likely on purpose and prove it with evidence. Sleeps, retries and "add a lock somewhere" usually move the bug rather than remove it.
</context>

<task>
Diagnose this concurrency bug.

Code:
[CODE]

Symptoms:
[SYMPTOMS]

Only if [RUNTIME] was provided: Runtime and concurrency model: [RUNTIME]
If the runtime or the concurrency model is not clear from the code, ask before going further, because the answer changes which interleavings are possible.

1. Map the concurrency: list each unit that runs concurrently (threads, goroutines, async tasks, workers, processes, app instances, cron jobs) and each piece of shared state (in-memory fields, caches, globals, files, database rows, queues, external resources). For each piece, list every read and write with its location and the synchronisation that protects it, if any.
2. Name the invariant that the symptom shows is broken (for example, "an order is charged at most once").
3. Enumerate candidate interleavings that break it. Check at least: check-then-act and read-modify-write without atomicity; lost updates in the database under the actual isolation level; publication without a happens-before edge (unsafe lazy init, non-volatile flags); iterating a collection while it is modified; await points that split a critical section in single-threaded async code; lock ordering that can deadlock; time-of-check to time-of-use on files or external state; duplicate delivery from retries or at-least-once queues. Write each candidate as a step-by-step timeline of A and B.
4. Rank candidates by how well they explain every symptom (frequency, load dependence, the exact wrong value). Drop those that contradict the evidence.
5. Propose instrumentation that can confirm or rule out the top candidates without hiding the bug: log lines with unit id, monotonic timestamp and a sequence or version number at each access; the runtime's race detector or concurrency checker if one exists for this runtime; a stress test that runs the operation concurrently many times, with injected delays or yields at the suspected gap to widen the window.
6. Propose the fix that removes the bad interleaving at its root, preferring in order: removing the sharing, making the operation atomic (a single atomic op, a conditional update, a unique constraint, a transaction at the right isolation level, optimistic locking with a version), then a lock with a documented scope and order. Make operations idempotent where duplicates are possible.
7. Define how to verify: the stress test fails before the fix at a measured rate and passes after many runs.
</task>

<constraints>
- Never propose sleeps, retries or longer timeouts as the fix.
- Do not claim a root cause is confirmed until the evidence from step 5 confirms it; until then, call it the leading hypothesis.
- Keep the fix as small as the root cause allows, and state what it costs (contention, throughput, latency).
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Shared state
Table: State | Readers and writers (location) | Protection.
## Candidate interleavings
Ranked. For each: the broken invariant, a two-column timeline (A | B), and how well it explains the symptoms.
## Instrumentation
What to add or run, and the result that would confirm or rule out each top candidate.
## Fix
The diff for the leading candidate, and why it removes the interleaving.
## Verification
The stress or race-detector test, how many runs, and the before and after failure rates to expect.
</output_format>
