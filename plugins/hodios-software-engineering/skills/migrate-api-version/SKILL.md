---
name: migrate-api-version
description: Plans a breaking API version change with a deprecation timeline, compatibility shims, a client migration guide and adoption telemetry. Use before changing anything clients rely on.
license: CC0-1.0
arguments:
  - current_api
  - changes
  - clients
argument-hint: <current_api> <changes> [clients]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: migration
  source: https://hermes-ide.com/prompts/migrate-api-version
  catalog: 2026.1004.1
---

# Plan a breaking API version change

## Inputs

- `current_api` (required): The current API - an OpenAPI or GraphQL schema excerpt, the versioning scheme in use, and public or internal audience.
- `changes` (required): The changes you want to make and why.
- `clients` (optional): Known clients - SDKs, mobile apps with slow update cycles, partners, internal services - and what you know about their usage.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Breaking an API costs every client time and trust, so the best breaking change is the one avoided: additive fields, accepting both old and new forms, expand-then-contract. When a break is necessary, it succeeds when there is one implementation behind a translation layer, a published timeline with machine-readable deprecation signals, telemetry that shows exactly who still uses the old behaviour, and a migration guide good enough that clients can upgrade without opening a support ticket.
</context>

<task>
Plan this API change.
Current API:
$current_api
Changes wanted:
$changes
Only if clients was provided: 
Known clients:
$clients

1. Classify each change as breaking or non-breaking. Breaking includes removed or renamed fields and endpoints, type or format changes, new required inputs, stricter validation, changed defaults, changed status or error codes, changed pagination, ordering or semantics, and authentication changes.
2. For each breaking change, look for a non-breaking route first: add the new field beside the old one, accept both inputs, or put the new behaviour behind an opt-in. Only what remains needs a new version.
3. Versioning: follow the scheme already in use (URL path, header, media type or dated versions). Bundle the remaining breaks into one version rather than several.
4. Compatibility layer: keep one implementation and translate old requests and responses at the edge, so the old version costs little to keep. Say which changes cannot be translated.
5. Timeline: announcement, the new version available, deprecation signals on old-version responses (the `Deprecation` and `Sunset` HTTP headers plus a link to the guide), brownouts (short scheduled failures to surface forgotten clients), and the sunset date. Size the window to the slowest client: mobile apps and partner integrations need far longer than internal services.
6. Telemetry: usage by version, endpoint and client identity, plus use of the specific fields or behaviours being removed. Set adoption targets for each milestone and a plan for contacting the clients who lag behind.
7. Write the client migration guide: for each change, before and after examples of requests and responses, the code change, how to test, and the dates.
</task>

<constraints>
- Do not invent clients or usage numbers. If clients are unknown, make adding telemetry the first milestone and give no sunset date until data exists.
- Never move the sunset date earlier once announced.
- Write the guide for the client developer: plain language and examples, no internal reasoning.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
</constraints>

<output_format>
## Change classification
A table: change, breaking (yes/no), who it affects, why.
## Avoid the break
For each breaking change, the non-breaking alternative or why there is none.
## Versioning
The decision and the version identifier.
## Compatibility layer
What is translated, where, and what cannot be.
## Timeline
A table: milestone, timing relative to announcement, what happens, communication.
## Telemetry
Metrics, dimensions, dashboards and adoption targets.
## Client migration guide
A ready-to-publish draft.
## Risks
Bullets with mitigations.
</output_format>
