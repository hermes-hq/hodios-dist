---
name: integrate-third-party-api
description: Implements a typed client for a third-party HTTP API from its docs, with auth, pagination, retries, rate limits and a test fake. Use when wiring an external service into your code.
license: CC0-1.0
arguments:
  - api_docs
  - operations
  - language
argument-hint: <api_docs> <operations> [language]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: implementation
  source: https://hermes-ide.com/prompts/integrate-third-party-api
  catalog: 2026.1003.1
---

# Integrate a third-party API

## Inputs

- `api_docs` (required): The API documentation, pasted or as a URL. Include the auth, pagination, rate-limit and error sections.
- `operations` (required): The API operations you need, for example "list customers, create invoice".
- `language` (optional): Language of the client. Leave empty to use the repo's main language.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Integrations break in production, not in the demo. The token expires mid-batch, page 2 never loads because the cursor was ignored, a 429 storm turns into a retry storm, a non-idempotent POST is retried and charges twice, a new field in the response crashes a strict parser, and the tests hit the real API. The client you write must hold up against all of that, and must not invent endpoints or fields the docs do not describe.
</context>

<task>
Build a client for the operations below in $language (if empty, use the repo's main language and its existing HTTP library).

Documentation: $api_docs
Operations needed: $operations

1. Read the docs (fetch them if given a URL). Extract, with section references: base URL and versioning, auth scheme, each needed operation's method, path, parameters and response fields, the pagination style, rate limits and their headers, error format, and idempotency support. List anything the docs leave unclear under Doc gaps; do not fill gaps with guesses.
2. Look for an existing HTTP wrapper, config loader, logger and error types in the repo and reuse them.
3. Design a small interface: one method per operation, typed inputs, typed results, and a typed error hierarchy (auth, not found, validation, rate limited, server, transport) that keeps the status code and the provider's request id.
4. Implement:
   - **Auth:** credentials from configuration, never hard-coded or logged. For OAuth, refresh before expiry and let only one refresh run at a time.
   - **Timeouts** on every request, for both connect and read.
   - **Retries** only for transport errors, 429, 502, 503 and 504, and only for idempotent methods or requests carrying an idempotency key. Use exponential backoff with full jitter, honour `Retry-After`, and cap both the attempts and the total time.
   - **Rate limits:** a client-side limiter sized to the documented limit, plus backing off when the rate-limit headers say so.
   - **Pagination:** a lazy iterator that follows the documented cursor, link header or offset, with a stop condition and a guard against a cursor that repeats.
   - **Parsing:** model only the fields you use, ignore unknown fields, and parse dates and money explicitly (money as decimal or minor units, never float).
5. Write a test fake implementing the same interface for callers' tests, and transport-level tests with canned responses for: success, multi-page listing, 429 with `Retry-After` then success, a 5xx retried then succeeding, a non-retryable 4xx, 401, and a malformed body.
6. Run the tests. Unit tests must make no real network calls.
</task>

<constraints>
- Every endpoint, field and header you use must appear in the docs. If one you need does not, stop and report it.
- Redact authorization headers, tokens and personal data from logs and error messages.
- Do not add an SDK or HTTP dependency the repo does not already use unless the docs require it. If the provider publishes an official SDK, mention it in one line under Operational notes.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Doc gaps
What the docs leave unclear and the assumption you made for each, or "None".

## Interface
The public methods with signatures, one line of purpose each.

## Changes
One line per file.

## Tests
One line per test: the scenario it covers.

## Configuration
| Setting | Env var | Default | Required |

## Operational notes
Rate limits, retry budget and worst-case latency per call, and what to monitor.
</output_format>
