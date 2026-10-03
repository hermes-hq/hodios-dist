---
name: add-rate-limiting
description: Adds rate limiting to API endpoints with a fitting algorithm, keys, per-tier limits, standard headers, 429 responses and tests. Use when protecting endpoints from abuse or overload.
license: CC0-1.0
arguments:
  - endpoints
  - traffic_profile
  - stack
  - storage
argument-hint: <endpoints> [traffic_profile] [stack] [storage]
disable-model-invocation: true
metadata:
  version: 1.1.0
  kind: prompt
  category: implementation
  source: https://hermes-ide.com/prompts/add-rate-limiting
  catalog: 2026.1003.0
---

# Add rate limiting to an API

## Inputs

- `endpoints` (required): The endpoints or route groups to protect and why, for example "POST /login (credential stuffing), /api/v1/* (fair use per API key)".
- `traffic_profile` (optional): Normal and peak request rates, clients (browsers, partners, mobile), plans or tiers, and whether traffic comes through a CDN or proxy.
- `stack` (optional): Language, framework and deployment (number of instances). Leave empty to detect it from the repo.
- `storage` (optional; one of: auto, in-memory, redis, memcached, database; default: auto): Where counters live. auto picks in-memory for a single instance and the shared store the app already has (usually Redis) when there are several; in-memory with several instances is only allowed as an explicit per-instance limit.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Rate limiting goes wrong in a few repeatable ways: limits keyed by client IP when every request arrives from the load balancer's address, or keyed by a spoofable X-Forwarded-For; login limits keyed by account and IP together, which a botnet rotating IPs walks straight past, or a hard per-account lockout that lets anyone lock a victim out; a limiter that blocks every login when its store goes down; in-memory counters on six instances that quietly allow six times the limit; a read-then-write counter in Redis that races under load; fixed windows that allow double the limit at the window boundary; 429 responses with no hint of when to retry, so clients hammer harder; and limits switched on in production without anyone knowing which customers they would block. Good rate limiting picks the key and algorithm per purpose, is atomic, tells clients what is happening and is rolled out in observe-only mode first.
</context>

<task>
Add rate limiting to these endpoints:

<endpoints>
$endpoints
</endpoints>

Only if traffic_profile was provided: 
Traffic profile: $traffic_profile
Only if stack was provided: 
Stack: $stack
Counter storage: $storage (auto: in-memory only for a single instance, otherwise the shared store the app already runs; ask before adding a new one)

1. Read the app's middleware chain, auth, proxy configuration, existing rate limiting (including at a gateway, CDN or WAF) and how many instances run. Do not add a second limiter on top of an existing one without saying why.
2. Define the policy per endpoint group, in a table:
   - **Purpose:** abuse prevention (login, sign-up, password reset, OTP), fair use per customer, or overload protection.
   - **Key:** authenticated user or API key for fair use. For login, password reset and OTP endpoints, two independent limits: one per target account identifier across all IPs (stops guessing one account from many IPs; slow it with growing delays or a challenge rather than a hard lockout an attacker can trigger on purpose) and one per client IP across all accounts (stops one source spraying many accounts). Client IP only when there is no identity, always derived from the trusted proxy hop (configure the framework's trusted-proxy setting rather than reading the header blindly). Say plainly that per-IP limits do not stop distributed credential stuffing, and name what complements them (breached-password checks, bot management at the CDN, MFA).
   - **Algorithm:** token bucket or GCRA when bursts are acceptable, sliding window (log or counter) when the limit must be smooth; avoid plain fixed windows unless the boundary burst is acceptable, and say so.
   - **Limits:** per tier or plan, with burst size. Propose numbers from the traffic profile with the reasoning, marked as proposed if no profile was given.
3. Implement it with the framework's middleware or a well-maintained library already in use or common for the stack. With a shared store, make the check-and-increment atomic (a single atomic command or a server-side script), set expiry on every key, and decide what happens when the store is unavailable: fail open for fair-use limits; for login-style endpoints fall back to a stricter per-instance in-memory limit rather than rejecting every login, which would turn a cache outage into an auth outage. Log and emit a metric either way.
4. Respond correctly: HTTP 429 with a `Retry-After` header, a consistent error body in the API's existing error format, and rate-limit headers on responses. Use the `RateLimit-Policy` and `RateLimit` header fields from the IETF HTTPAPI draft if the API has no existing convention, or the widely used `X-RateLimit-Limit`, `X-RateLimit-Remaining` and `X-RateLimit-Reset` if clients already expect those; say which and why.
5. Add allowlisting for health checks and internal callers where needed, and make limits configurable without a deploy.
6. Add observability: a metric of allowed and limited requests by endpoint group and tier, and a log line for limited requests with the key hashed or truncated.
7. Write tests with a fake or controllable clock: requests under the limit pass, the limit plus one returns 429 with Retry-After, the bucket refills over time, different keys do not interfere, tiers get their own limits, the spoofed X-Forwarded-For case does not bypass the limit, and the store-down behaviour matches the chosen policy. Run them and report the real result.
8. Recommend a rollout: log-only (shadow) mode first, review who would have been limited, then enforce.
</task>

<constraints>
- Do not use in-memory counters when there is more than one instance unless the limit is explicitly per instance; say so if it is.
- Never key on a client-supplied header without a trusted-proxy configuration.
- Keep limits and tier names in configuration, not hard-coded in handlers.
- Do not claim a header draft is a final standard; describe it as the IETF draft.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Policy
Table: endpoint group, purpose, key or keys, algorithm, limit and burst per tier, store-down behaviour. Proposed numbers are marked proposed.
## Design
Where the limiter sits in the request path, the storage and atomicity approach, and the headers, in a few bullets.
## Changes
One line per file.
## Tests
One line per test and the real result of the run.
## Rollout
Numbered steps from shadow mode to enforcement, with what to watch.
</output_format>
