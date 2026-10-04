---
name: instrument-service-observability
description: Plans and adds logs, metrics and traces using OpenTelemetry conventions, golden signals, useful log fields, cardinality limits and first dashboards. Use when a service is hard to debug in production.
license: CC0-1.0
arguments:
  - service
  - stack
  - existing_tooling
argument-hint: <service> [stack] [existing_tooling]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: incident
  source: https://hermes-ide.com/prompts/instrument-service-observability
  catalog: 2026.1004.3
---

# Instrument a service for observability

## Inputs

- `service` (required): What the service does, its main endpoints, jobs or consumers, its dependencies (databases, queues, other services), and the production questions nobody can answer today.
- `stack` (optional): Language, framework and runtime (for example Python 3.12 with FastAPI, Java 21 with Spring Boot).
- `existing_tooling` (optional): What is already in place - log shipping, metrics backend, tracing, APM vendor, OpenTelemetry Collector - and any constraints on cost or vendors.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Services are hard to debug in production when logs are unstructured text with no request or trace id, metrics are averages that hide the slow tail, traces stop at the first queue or thread hop, and nobody can tell whether the last deploy is to blame. The opposite failure is just as common: user ids and raw URLs as metric labels that explode cardinality and cost, debug logging left on, and personal data in log lines. Good instrumentation starts from the questions on-call engineers need answered and uses standard names (OpenTelemetry semantic conventions) so the data works with any backend.
</context>

<task>
Instrument this service:
$service
Only if stack was provided: 

Stack: $stack
Only if existing_tooling was provided: 

Existing tooling: $existing_tooling

1. If the code is available, read the entry points, the outbound calls, the background work and any existing logging or metrics setup before proposing changes.
2. List the production questions the telemetry must answer: is it healthy right now, which endpoint or dependency is slow or failing, is it the last deploy, which tenant or customer segment is affected, is it running out of a resource.
3. Traces: start with the OpenTelemetry SDK and the auto-instrumentation available for this stack (HTTP server and client, database driver, message queue). Add manual spans only around meaningful business operations and expensive internal steps. Propagate W3C trace context across every hop, including queues and background jobs. Set resource attributes (`service.name`, `service.version`, deployment environment) and a sampling policy: a head-based ratio, plus keeping all errors and slow traces if a collector can do tail-based sampling.
4. Metrics: request rate, errors and duration per route template for each request-driven interface; the same for each outbound dependency; saturation for the resources that limit this service (connection pools, worker queues, thread or event-loop lag, memory). Use histograms for durations with buckets around the latency targets. Follow the OpenTelemetry semantic-convention names for the stack's instrumentations, and check the current names in the conventions, since some have changed between versions.
5. Logs: structured (JSON) with a fixed set of fields on every line (timestamp, level, message, service, version, environment, `trace_id`, `span_id`) plus event-specific fields; log levels with clear meaning; one log line per error with the error type and stack trace; and no secrets, tokens or personal data (list what to redact or hash).
6. Cardinality limits: metric labels only from bounded sets (route templates, status class, dependency name, region). User ids, request ids, raw URLs, emails and error messages go on spans and logs, never on metric labels. Estimate the series count per metric.
7. Export through an OpenTelemetry Collector where possible, so the backend can change without code changes.
8. Define the first dashboards (service overview with rate, errors and latency per route, dependencies, saturation, and deploy markers) and two to four alerts on user-facing symptoms, not on causes.
9. Write the code changes for the stack: SDK setup, configuration by environment variables, the log formatter, the custom spans and metrics, and context propagation for any queue.

If the stack is unknown and the code is not available, ask for it before writing code; the plan can still be written.
</task>

<constraints>
- Prefer standard OpenTelemetry APIs and semantic conventions over vendor SDKs, and say where a vendor-specific step is unavoidable.
- No unbounded label values on metrics. No personal data or secrets in any signal.
- Instrument what answers the questions in step 2; do not add spans or metrics with no consumer.
- Keep the overhead visible: say what the sampling ratio and log volume will cost relative to traffic, as a formula if the numbers are unknown.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Questions to answer
Numbered list, each mapped to the signal that answers it.

## Plan
Ordered rollout steps, smallest useful step first.

## Traces
Auto-instrumentation, manual spans (name and attributes) and the sampling policy.

## Metrics
Table: name | type | unit | labels | question it answers.

## Logs
The required fields, levels, and the redaction list.

## Code changes
Code blocks per file in the target stack.

## Dashboards and alerts
Panels for the first dashboard, and each alert with its condition and why it matters to users.

## Verification
How to send one request and find it in logs, metrics and traces, linked by `trace_id`.

## Cost and cardinality
Estimated series per metric, log volume and trace sampling, and the levers to cut each.
</output_format>
