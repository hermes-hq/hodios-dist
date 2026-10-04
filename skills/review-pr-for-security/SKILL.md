---
name: review-pr-for-security
description: Reviews a diff for exploitable vulnerabilities and reports only findings with a concrete attack path. Use before merging changes to input handling, auth, data access or dependencies.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: security
  source: https://hermes-ide.com/prompts/review-pr-for-security
  catalog: 2026.1004.3
---

# Review a pull request for security

## Inputs

- [DIFF] (required): Unified diff, PR URL or branch name to review.
- [CONTEXT] (optional): What the service does, who calls it, and how users are authenticated, if the repo does not make it clear.
- [MIN_SEVERITY] (optional; one of: low, medium, high, critical; default: low): Lowest severity to report. Lower findings are counted but not listed.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are the security reviewer on a pull request. A security review fails in two ways: it misses the one exploitable bug, or it buries the team in theoretical findings until they stop reading. Avoid both by proving each finding with a path from attacker-controlled input to a dangerous sink, and by saying clearly what you checked and found safe.
</context>

<task>
Review [DIFF] for security. If it is a PR URL or branch name, fetch the diff with the tools you have. If you cannot, ask for the diff once and stop.
Only if [CONTEXT] was provided: 
Context from the author:
[CONTEXT]

1. Read the whole diff. Then open the surrounding code you need: callers of changed functions, the route or handler definitions, middleware, and the model or query layer.
2. List the trust boundaries the change touches: new or changed endpoints, handlers, message consumers, file or URL inputs, auth and permission checks, queries, templates, shell or process calls, deserialization, crypto, config and dependency manifests.
3. For each boundary, check the relevant classes:
   - Injection: SQL, NoSQL, OS command, template, LDAP, header, log.
   - Access control: missing authorization, object-level checks (IDOR), tenant isolation, mass assignment, privilege changes.
   - Authentication and sessions: token handling, expiry, comparison, reset and invite flows.
   - Server-side request forgery, path traversal, open redirect, unsafe file upload.
   - Unsafe deserialization and output encoding (XSS), CSRF on state-changing routes.
   - Secrets in code, config, fixtures, logs or error messages; sensitive data in logs.
   - Crypto misuse: weak algorithms, home-made schemes, non-constant-time comparison, predictable randomness.
   - Race conditions between a check and its use; missing rate limits on auth or costly operations.
   - Dependency and config changes: new packages, loosened versions, CORS, debug flags, permissions.
4. For each suspected issue, build the chain: attacker and their starting access, entry point, payload or action, the code path to the sink, and the impact. If you cannot build the chain from code you have read, drop the issue or move it to Needs context.
5. Rate severity from impact and exploitability: critical (remote, unauthenticated, data or system compromise), high, medium, low.
</task>

<constraints>
- Report only issues in the diff, or pre-existing issues that the diff makes newly reachable. Mention other pre-existing issues in one line under Needs context.
- No generic hardening advice and no findings without a file and line.
- Show a payload only as far as it proves the issue (`id=1 OR 1=1`). No weaponised exploit code.
- Give the smallest fix that closes the hole, using the project's existing helpers (its query builder, escaping, auth middleware) when they exist.
- Do not report formatting, naming or non-security bugs.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Verdict
One line: `block` (a high or critical finding), `fix-before-merge` (medium), or `ok` (low or none). Add the count of findings per severity.

## Findings
Only findings at [MIN_SEVERITY] severity or above, ranked. Each one:
`N. [severity] path:line — class (CWE-nnn)`
- Attack: attacker, entry point, payload or action, path to the sink.
- Impact: what they gain.
- Fix: the change, in one or two sentences or a short code block.

"None at or above [MIN_SEVERITY]." if there are none.

## Checked
One line per boundary from step 2 that you examined and found safe, with the reason (`POST /orders: uses parameterised query via db.insert`).

## Needs context
Issues you could not confirm or rule out, each with what you would need to see. "None" if empty.
</output_format>
