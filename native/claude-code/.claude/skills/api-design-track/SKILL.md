---
name: api-design-track
description: Takes a new API from consumer needs to a resource model, a reviewed contract, error and versioning rules, and a mock with contract tests, pausing for approval between steps.
license: CC0-1.0
arguments:
  - consumers
  - constraints
  - style
argument-hint: <consumers> [constraints] [style]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: architecture
  source: https://hermes-ide.com/prompts/api-design-track
  catalog: 2026.1004.3
---

# API design track

## Inputs

- `consumers` (required): Who will call the API (public developers, partners, mobile apps, internal services) and what each needs to accomplish with it.
- `constraints` (optional): Fixed constraints such as existing conventions, auth system, data residency, SLAs, launch date or systems the API must sit in front of.
- `style` (optional; one of: rest, graphql, grpc; default: rest): API style for the contract.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Designs a $style API for these consumers, one approved step at a time:

<consumers>
$consumers
</consumers>

Only if constraints was provided: 
<constraints>
$constraints
</constraints>

A public or partner API is expensive to change once clients depend on it, so the contract is designed from the consumers' side and reviewed before any server code exists. Each step produces one artifact and stops for the API owner's approval; later steps build on approved versions instead of re-asking. Never invent business rules, limits, permissions or prices: mark them as assumptions or questions. Given constraints and conventions override the defaults in the steps.

## Steps

Work through these steps in order. Do not skip a gate.

1. consumer-needs (discover)
2. resource-model (design)
3. contract (design)
4. errors-and-versioning (design)
5. mock-and-contract-tests (verify)

### Step 1: Consumer needs

Understand who will call the API and what they must get done before modelling anything.

1. If essentials are missing, ask for them in one message and wait: consumer types and counts, the jobs each must accomplish (for example "sync new orders into our ERP every five minutes"), their environment (server, browser, mobile on flaky networks, low-code tools), auth, volumes and latency needs, and data they must never see.
2. Write a consumer needs brief:
   - **Consumers:** table of consumer, environment, auth, volume and jobs.
   - **Jobs:** numbered, phrased from the consumer's side, each with frequency and the cost of failure.
   - **Interaction patterns:** request and response, bulk, long-running operations, webhooks or events, offline sync, and which jobs need each.
   - **Non-goals** for the first version.
   - **Quality needs:** latency, availability, rate limits and freshness per job, marked stated or assumed.
3. List open questions with who should answer each.

Stop and wait for approval or edits. Do not model resources yet.

**Gate:** stop here and wait for the user's approval before step 2 (resource-model).

### Step 2: Resource model

Turn the approved jobs into a small, consistent model.

1. Identify the resources (GraphQL types, or gRPC services and messages) the jobs need, named in the consumers' domain language. Keep internal tables, identifiers and implementation-only states out.
2. For each resource: a one-line definition, its id (opaque strings by default), key fields with types, read-only or server-generated fields, lifecycle states, and relationships (embedded, referenced or sub-resource).
3. Map every job to the operations it needs. Flag jobs that take more than two or three calls and propose a better-shaped or bulk operation if justified.
4. Fix the $style conventions: naming case, timestamps (RFC 3339, UTC), money (integer minor units plus ISO 4217 code), cursor pagination, filtering and sorting, and long-running operations.
5. Draw the model as a Mermaid class diagram, and note per resource which consumer may read or change what and which fields are sensitive.

Stop and wait for approval or edits. Do not write the contract yet.

**Gate:** stop here and wait for the user's approval before step 3 (contract).

### Step 3: Contract

Write the machine-readable contract for the approved model.

1. One fenced block: OpenAPI 3.1 YAML for REST, SDL for GraphQL, or proto3 for gRPC, per the $style choice and approved conventions.
2. For every operation: request and response schemas with types, required fields, formats and constraints; the auth scope; whether it is idempotent; one realistic example. Creates and money movements accept an idempotency key. Lists are paginated with a maximum page size. Racing updates use optimistic concurrency (ETag and If-Match, or a version field).
3. Review the contract and list findings in a table (issue, location, fix): inconsistent naming, chatty flows, leaked internals, ambiguous nullability, booleans that will need a third state, enums consumers cannot handle growing, missing examples. Apply confident fixes; list the rest as questions.
4. List every assumption the contract relies on.

Stop and wait for approval or edits. Do not write error or versioning rules yet.

**Gate:** stop here and wait for the user's approval before step 4 (errors-and-versioning).

### Step 4: Errors and versioning

Define how the API fails and how it changes over time.

1. **Error model.** One shape for every operation: RFC 9457 problem details plus a stable machine-readable code and field errors for REST; the errors array with `extensions.code` for GraphQL; standard status codes with structured details for gRPC. Follow given conventions if they differ.
2. **Error catalogue.** Table: code, status, when it happens, retryable, what the client should do. Cover validation, authentication, authorization, not found, conflict, idempotency key reused with a different body, rate limiting (with Retry-After), dependency failure and unexpected errors. Never leak stack traces, internal ids or other tenants' data.
3. **Compatibility rules.** Non-breaking: new optional fields and operations, new enum values only if consumers were told to tolerate unknown ones. Breaking: removing or renaming fields, changing types or defaults, tightening validation, changing error codes.
4. **Versioning.** Choose and justify one scheme (path or package version, date-based header, or versionless evolution for GraphQL), the support period for old versions, and how deprecation is signalled (Deprecation and Sunset headers, schema or field deprecation markers) and announced.
5. Show the changed parts of the contract.

Stop and wait for approval or edits. Do not build the mock yet.

**Gate:** stop here and wait for the user's approval before step 5 (mock-and-contract-tests).

### Step 5: Mock and contract tests

Give consumers something to build against and the team a check that keeps the implementation honest.

1. **Mock.** Recommend how to serve a mock generated from the approved contract and keep it in sync. Include realistic data for every operation and a way for consumers to trigger each catalogued error (for example a test header or magic id).
2. **Contract tests** that fail when the implementation drifts: every response, including errors, validated against the contract; per operation, the happy path, a validation error, an authorization failure and, where relevant, idempotent retry, pagination to the last page and a concurrency conflict; and a CI check that fails on breaking changes against the last released contract. Use the project's test framework if named; otherwise pick a common one and say which.
3. If consumers are internal teams, propose consumer-driven contract tests in the provider's pipeline.
4. **Hand-off checklist:** contract reviewed and versioned, mock published, contract tests in CI, error catalogue and changelog published, rate limits documented, owner and support channel named.

This is the last step. List the open questions that still block a first release, each with an owner.
