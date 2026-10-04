---
name: observability-setup-track
description: Instruments a service in gated steps with structured logs, metrics, traces, correlation ids, business metrics, dashboards as code and a verification run. Use when a service is a black box.
license: CC0-1.0
arguments:
  - service_path
  - stack
  - backend
argument-hint: <service_path> <stack> [backend]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: incident
  source: https://hermes-ide.com/prompts/observability-setup-track
  catalog: 2026.1004.2
---

# Add logs, metrics and traces to a service

## Inputs

- `service_path` (required): Path to the service in the repository, for example "services/orders".
- `stack` (required): The service's language and framework, for example "Python FastAPI with Celery workers" or "Java Spring Boot".
- `backend` (optional; default: open-standards): Where telemetry goes. "open-standards" means OpenTelemetry SDKs exporting OTLP, Prometheus-style metrics and dashboards for a Grafana-compatible tool; or name the vendor or stack already in use.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Makes the $stack service at `$service_path` observable, exporting to $backend. The goal is that the next incident can be answered from telemetry: which requests fail, since when, for whom, and where the time goes. Instrumentation goes wrong in predictable ways: unstructured log lines nobody can query, a metric label holding user ids that explodes cardinality and cost, traces that break at every queue or thread hop, and personal data copied into logs. This track plans first, then wires logs, metrics and traces through the libraries the service already uses, and proves the signals arrive.

Rules for every step:
- Follow the service's existing logger, config and dependency injection patterns; extend rather than replace.
- No personal data or secrets in telemetry: no names, emails, addresses, tokens, passwords, full request or response bodies, or payment data in logs, metric labels or span attributes. Use ids that are not personal, or hash where joining is needed, and redact at the logger or exporter level so a new log line cannot leak by accident.
- Every metric label has a bounded set of values. User ids, request ids, raw URLs and error messages are never labels.
- Telemetry must never break the request path: exporter failures are logged and dropped, not raised.
- Use OpenTelemetry semantic conventions for names and attributes where they exist.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.

## Steps

Work through these steps in order. Do not skip a gate.

1. survey (discover)
2. logging (build)
3. metrics-traces (build)
4. dashboards (build)
5. verify (verify)

### Step 1: Survey and plan

1. Find what exists: logging library and format, any metrics or tracing libraries, request id handling, health endpoints, existing dashboards or alert files, and how config and secrets reach the service.
2. List the entry points (HTTP routes, RPC handlers, queue consumers, scheduled jobs, CLI commands) and the outbound calls (databases, caches, HTTP clients, queues, third-party APIs).
3. Name the key business operations from the code and docs (for example "order placed", "payment captured", "export completed") and what success and failure mean for each.
4. Propose the plan:
   - Log schema: the fields every line carries (timestamp, level, service, environment, version, trace and span id, request or job id, operation, outcome, duration) and the levels policy.
   - Metrics: request rate, errors and duration per route or operation (histograms with explicit buckets around the latency that matters); saturation for pools, queues and workers; the business metrics; each with name, unit, type and its bounded labels, plus a cardinality estimate.
   - Traces: automatic instrumentation for the framework and clients in use, manual spans around key operations, propagation across queues and background jobs, sampling choice.
   - Data protection: fields that must be redacted or dropped.

Write the artifact: Current state, Entry points and dependencies, Business operations, Log schema, Metrics (Name | Type | Unit | Labels | Cardinality | Question it answers), Traces, Redaction list, Sampling. Stop and wait for approval.

Save this step's result to `observability/01-plan.md`.

**Gate:** stop here and wait for the user's approval before step 2 (logging).

### Step 2: Structured logging and correlation

1. Configure the existing logger (or the standard structured logger for $stack if there is none) to emit one JSON object per line to stdout with the approved fields.
2. Add or reuse middleware that accepts an incoming W3C `traceparent` (and an existing request id header if the platform uses one), creates one when missing, puts it in the logging context, and returns the request id in the response.
3. Carry the context into background jobs and queue messages so a job's logs link to the request that enqueued it.
4. Add the redaction filter from the plan at the logger level and a test that proves a sample secret and email are removed.
5. Replace prints and string-built log lines on the main paths with structured calls carrying fields, not interpolated text. Log each request or job once at completion with outcome and duration, and errors once with the stack trace where they are handled.

Continue to step 3.

### Step 3: Metrics and traces

1. Add the OpenTelemetry SDK (or the approved $backend equivalent) with configuration from environment variables: service name, version, environment, exporter endpoint, sampling ratio. Default to a console or no-op exporter when no endpoint is set so local runs and tests need nothing extra.
2. Enable automatic instrumentation for the framework, HTTP clients, database drivers and queue clients the service uses.
3. Add manual spans around the key business operations, with attributes that help debugging and contain no personal data, and record exceptions on spans.
4. Register the approved metrics: request and operation duration histograms, error counts by bounded error class, saturation gauges, and business counters. Expose them the way the backend expects (a scrape endpoint or OTLP push).
5. Expose liveness and readiness checks if missing: liveness says the process is up; readiness checks the dependencies needed to serve.

Continue to step 4.

### Step 4: Dashboards as code

1. Use the dashboards-as-code format the team already has (dashboard JSON in the repo, a provisioning folder, Terraform, Jsonnet or the vendor's config format). If there is none, write a dashboard JSON for a Grafana-compatible tool and say how to import it.
2. One overview dashboard: request rate, error ratio and latency percentiles per route or operation; saturation; business metrics; a panel of recent error logs filtered by trace id. Every panel title states the question it answers.
3. Write the queries against the metric names actually registered in step 3.
4. Propose, but do not activate, two or three alert conditions tied to user impact (error ratio and latency on the key operations), each with a threshold placeholder for the team to set with an SLO.

Continue to step 5.

### Step 5: Verify the signals

1. Run the service locally with a local collector or the console exporter (a compose service is fine). Exercise the main routes, one failing request, and one background job.
2. Confirm and record, with snippets:
   - Logs are JSON, carry the approved fields, and share one trace id across the request and the job it enqueued.
   - Metrics appear with the expected names, units and labels, and label values stay bounded.
   - Traces connect from the entry point through database and outbound calls, with no broken parent links at queue hops.
   - The redaction test passes, and a search of the captured output finds no emails, tokens or passwords.
   - The service still runs and passes its tests with the exporter endpoint unreachable.
3. Run the project's test suite and linters.

Write the report:

#### Signals
What is now logged, measured and traced, per entry point and operation.

#### Verification
Each check above with its real result and a short snippet.

#### Configuration
Environment variables added, with defaults.

#### Dashboards and alerts
Files written and how to load them; proposed alerts awaiting thresholds.

#### Follow-ups
Gaps, such as services downstream that do not propagate context, or SLOs to define.

Save this step's result to `observability/05-report.md`.
