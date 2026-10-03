---
name: write-integration-tests
description: Writes integration tests that run against real dependencies such as databases and queues in containers, with fixtures, isolation between tests and cleanup. Use when mocks hide bugs at the boundary.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: testing
  source: https://hermes-ide.com/prompts/write-integration-tests
  catalog: 2026.1003.0
---

# Write integration tests with real dependencies

## Inputs

- [CODE] (required): The code under test (repository, service, handler or worker) and how it is wired, or the path to it.
- [DEPENDENCIES] (optional): The real dependencies to run, with versions matching production, for example "Postgres 16, Redis 7, RabbitMQ 3.13".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Integration tests exist to catch what mocks cannot: SQL that only fails on the real engine, transaction and locking behaviour, migrations, serialisation across a queue, unique constraints, time zones and encodings. They become a burden when they share state and fail in random order, sleep instead of waiting, start a fresh container per test and take twenty minutes, or test the dependency rather than the code. Good integration tests start each dependency once per run, give every test its own data, wait on conditions, and assert on observable outcomes.
</context>

<task>
Write integration tests for:
<code>
[CODE]
</code>
Only if [DEPENDENCIES] was provided: 
Dependencies: [DEPENDENCIES]

1. Read the code and the project's existing test setup (framework, runner, folders, helpers, migrations, CI config). Follow what exists. If you cannot see the code or the dependency versions, ask once for what is missing and stop.
2. Write a short test plan: the behaviours that cross a real boundary (queries with filtering and ordering, constraint violations, transactions and rollbacks, concurrent updates, message publish and consume, retries and dead-lettering, cache expiry), each with the outcome to assert. Leave pure logic to unit tests.
3. Set up dependencies in containers, preferring the Testcontainers library for the language, or a compose file the test run starts. Pin image versions to match production. Start each container once per test run or suite, not per test. Apply the real schema migrations, not a hand-written schema.
4. Isolate tests. Pick the cheapest strategy that is correct and say why: a transaction per test rolled back at the end (not valid when the code under test commits or uses several connections), a unique schema, database, queue or key prefix per test or worker, or truncating tables between tests. Make tests safe to run in parallel or mark them serial.
5. Build data with small factories or builders that set only the fields a test cares about. No shared mutable fixtures.
6. Wait on conditions with a timeout (poll until the message is consumed, up to a few seconds); never fixed sleeps.
7. Clean up containers, connections and temporary resources even when a test fails.
8. Run the tests and report the real result. If you cannot run them (no container runtime), say so plainly.
</task>

<constraints>
- Use the real dependency for the behaviour under test; mock only external third parties you do not control, and say which.
- Never point tests at a shared or production environment, and never read real credentials. Use container-generated connection settings.
- Assert on outcomes (rows, messages, responses), not on which internal functions were called.
- Fix the behaviour, not the test. Never special-case test inputs, weaken assertions or skip tests to make a check pass.
- If a test looks wrong, explain why and ask before changing it.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Test plan
A table: behaviour, dependency, assertion.
## Setup
The container or compose setup and shared fixtures, as code blocks with file paths.
## Tests
The test files, as code blocks with file paths.
## How to run
Commands for local runs and the CI job change, plus the result of running them.
## Notes
Isolation strategy chosen and why, expected runtime, and anything that could make the tests flaky.
</output_format>
