---
name: plan-load-test
description: Designs a load test with a workload model, scenarios, ramp profile and pass or fail thresholds, then writes the script for the chosen tool. Use before a launch, a traffic event or a capacity decision.
license: CC0-1.0
metadata:
  version: 1.0.1
  kind: prompt
  category: performance
  source: https://hermes-ide.com/prompts/plan-load-test
  catalog: 2026.1004.3
---

# Plan a load test

## Inputs

- [SYSTEM] (required): The system under test - endpoints or user flows, architecture, auth, dependencies, and the question the test must answer.
- [TRAFFIC_PROFILE] (optional): Production traffic shape - peak requests per second or concurrent users, endpoint mix, daily pattern, expected growth or event peak.
- [TOOL] (optional; one of: k6, locust, jmeter, gatling; default: k6): Load testing tool to write the script for.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Most load tests answer the wrong question. They hammer one endpoint with a fixed number of looping users, hit only cached data, and report an average latency. Closed-model loops slow down when the system slows down, which hides the very saturation the test was meant to find (coordinated omission). A useful test models real arrival rates and the real mix of requests, uses varied data, and ends with a clear pass or fail against agreed thresholds.
</context>

<task>
Design a load test for:
[SYSTEM]
Only if [TRAFFIC_PROFILE] was provided: 
Production traffic:
[TRAFFIC_PROFILE]

1. State the objective as a question the test answers, such as "Does checkout meet p95 below 800 ms at 2x last Black Friday peak?". If the system description does not reveal the question, ask and stop.
2. Build the workload model: an open model with arrival rates (requests or iterations per second) for user-facing traffic; the mix of transactions by weight; think time; test data variety large enough to defeat caches the way real traffic does; authentication handling. If traffic data is missing, propose numbers, label them assumptions, and say how to derive the real ones from access logs.
3. Define scenarios: a smoke test, load at expected peak, a stress test that ramps past peak to find the breaking point, a spike, and a soak of several hours when leaks or slow degradation are a concern. Give the ramp for each.
4. Set pass and fail thresholds: latency percentiles (p95 and p99, never only the average), error rate, and the throughput achieved versus the target. List the server-side saturation signals to watch (CPU, memory, connection pools, queue depth, database load).
5. Write the script for [TOOL] implementing the model, the scenarios and the thresholds as automatic pass or fail where the tool supports it.
</task>

<constraints>
- Never point the test at production or at third-party services (payment providers, email, SMS) without explicit approval; stub or sandbox them and say so.
- Check the load generator itself is not the bottleneck, and say how.
- Exclude warm-up from the results.
- Do not invent endpoints or payloads; use placeholders where the description has none and list them.
</constraints>

<output_format>
## Objective
The question, and the decision it informs.
## Workload model
A table: transaction, share of traffic, target rate at peak, think time, test data source.
## Scenarios
A table: scenario, ramp, duration, purpose.
## Pass and fail criteria
A table: metric, threshold, source (client or server).
## Script
One fenced block for [TOOL], followed by any placeholders to fill.
## Run checklist
Environment parity, data reset, monitoring in place, people to notify, and how to abort.
</output_format>
