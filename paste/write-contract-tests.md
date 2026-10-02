<context>
Contract tests catch the integration bug where each service passes its own tests but the provider renames a field, tightens validation or changes a status code that a consumer depends on. In consumer-driven contracts the consumer records only what it actually sends and reads, so the provider is free to change everything else. Contracts that copy whole responses with exact values are brittle and block harmless changes; contracts that are never verified against the real provider, or never gate a deploy, catch nothing.
</context>

<task>
Write contract tests using the pact approach.

Consumer:
[CONSUMER]

Provider API:
[PROVIDER_API]

1. List each interaction the consumer really uses: method, path, query, headers that matter, request body fields, the response status and only the response fields the consumer reads. Trace field reads in the consumer code; do not include fields it ignores. Include the error responses the consumer handles (404, 409, 422 and so on).
2. For each interaction, name the provider state it needs ("order 42 exists and is paid").
3. Consumer side: write tests that exercise the real client code against the contract mock and check the client's own parsing, not just the mock. Use type and format matchers (like-type, regex, each-like with a minimum) instead of literal values, except where the exact value is the contract (enums, status codes).
4. Provider side: write the verification that replays the contract against the running provider, with a state handler per provider state that sets up data through the provider's own code or test fixtures.
5. CI: show how the contract is published (with consumer version and branch), how the provider verifies on every build, and the pre-deploy check that blocks a deploy when the deployed counterpart's contract is not verified (for Pact, a broker or PactFlow with `can-i-deploy --to-environment`, `record-deployment` after each deploy so the broker knows what runs where, and a contract-changed webhook that triggers provider verification). For openapi-schema, validate consumer mocks against the spec and provider responses against the spec, and fail on spec drift. For custom, store fixtures in one place both builds read, and version them.
6. Show one concrete breaking change (a renamed field, say) and which check fails.
</task>

<constraints>
- Do not invent endpoints, fields or status codes that are not in the inputs. If the provider API and the consumer disagree, report the mismatch as a finding instead of choosing one.
- Contracts are not functional tests: do not assert business rules of the provider beyond the shape and semantics the consumer relies on.
- Use the client library and test runner the consumer already uses. Name any package to install with its ecosystem.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
</constraints>

<output_format>
## Interactions
Table: Interaction | Request | Response fields used | Provider state.
## Consumer tests
Complete test file(s) in code blocks.
## Provider verification
Complete verification test with state handlers.
## CI gate
The pipeline steps (as config or a numbered list) for publish, verify and the pre-deploy check, and the breaking-change example.
## What this does not catch
Bullets: behaviour contract tests miss here (performance, auth flows, data semantics) and what covers it instead. Mismatches found between consumer and provider go first, if any.
</output_format>
