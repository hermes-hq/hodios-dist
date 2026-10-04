---
name: implement-background-job
description: Implements a background or scheduled job with idempotency, retries with backoff, dead-letter handling, timeouts, concurrency limits and observability. Use to move slow work off the request path.
license: CC0-1.0
arguments:
  - job_description
  - queue_or_scheduler
  - stack
  - volume
argument-hint: <job_description> [queue_or_scheduler] [stack] [volume]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: implementation
  source: https://hermes-ide.com/prompts/implement-background-job
  catalog: 2026.1004.2
---

# Implement a background job

## Inputs

- `job_description` (required): What the job does, what triggers it (an event, a user action or a schedule), its inputs and its side effects.
- `queue_or_scheduler` (optional): Queue or scheduler to use, for example Sidekiq, Celery, BullMQ, SQS, Cloud Tasks, Kubernetes CronJob or plain cron. Leave empty to use what the repo already has.
- `stack` (optional): Language and framework. Leave empty to detect it from the repo.
- `volume` (optional): Expected volume and timing, for example "50k jobs per day, bursts of 5k after the nightly import".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Background jobs fail quietly. Queues deliver at least once, so a job that runs twice sends two emails or charges twice. Retries without backoff turn a dependency outage into a self-inflicted load spike. A job with no timeout holds a worker forever; one with no concurrency limit exhausts the database pool. Scheduled jobs overlap when a run is slower than the interval, double-run when two instances each fire the same cron, or silently stop running and nobody notices for weeks. Payloads that carry full objects go stale between enqueue and execution. A job is production-ready when running it twice is safe, failure is visible and a stuck or poisoned job cannot take the system down.
</context>

<task>
Implement this job:

<job>
$job_description
</job>

Only if queue_or_scheduler was provided: 
Queue or scheduler: $queue_or_scheduler
Only if stack was provided: 
Stack: $stack
Only if volume was provided: 
Volume: $volume

1. Read how the repo already runs background work: the queue library, worker processes, job base classes, scheduling, config, logging and metrics. Reuse them. If there is none and none was named, recommend the simplest option that fits the stack and volume, say why, and ask before adding new infrastructure.
2. Design the job before coding and state it briefly:
   - **Trigger and payload:** enqueue after the triggering transaction commits (or through an outbox), and pass ids, not whole objects, so the job reads current state.
   - **Idempotency:** how running the same job twice is safe: a unique job key or dedup table, state checks before acting ("already sent"), upserts, and idempotency keys on outbound calls.
   - **Retries:** which errors are retryable (timeouts, 429, 5xx, lock contention) and which are not (validation, not found); exponential backoff with jitter; a maximum attempt count and total retry window.
   - **Dead letters:** where jobs go after the last retry, with the error and payload, and how they are inspected and replayed.
   - **Timeouts and limits:** a per-job timeout below the queue's visibility or lease timeout, a concurrency limit sized to the downstream capacity (database pool, API rate limit), and batching for large volumes with checkpoints so a crash resumes instead of restarting.
   - **Scheduling (if periodic):** exactly one run per interval across instances (scheduler-level uniqueness or a distributed lock with expiry), no overlap with a slow previous run, explicit time zone, and what happens to missed runs.
3. Implement the job, its enqueueing or schedule, and the configuration, following the repo's conventions.
4. Add observability: structured logs with job id, attempt and duration; metrics for enqueued, succeeded, failed, retried, dead-lettered, duration and queue latency; and for scheduled jobs a heartbeat or last-success timestamp that can be alerted on when it goes stale.
5. Write tests: the happy path; running the same job twice produces one side effect; a retryable error retries and then succeeds; a non-retryable error does not retry; exhausting retries dead-letters the job; the timeout fires; and for scheduled jobs, the overlap and uniqueness guard. Use the queue library's test mode or an in-memory fake; no real external calls.
6. Run the tests and linter and report the real results.
</task>

<constraints>
- Do not add a new queue, scheduler or dependency without saying why the existing ones do not fit, and ask first if it needs new infrastructure.
- Never put secrets or personal data in job payloads or logs; pass ids.
- Graceful shutdown: a worker that receives a stop signal finishes or releases its current job instead of dropping it.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Design
Bullets for trigger, payload, idempotency, retries, dead letters, timeouts and concurrency, and scheduling, each one line.
## Changes
One line per file.
## Tests
One line per test and the real result of the run.
## Configuration
| Setting | Default | Why |
## Operational notes
How to monitor it, which alerts to add, how to replay dead-lettered jobs, and how to pause or drain it safely.
</output_format>
