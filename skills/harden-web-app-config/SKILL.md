---
name: harden-web-app-config
description: Produces hardened HTTP security headers, a Content Security Policy, CORS and cookie settings for a web app, rolled out first in report-only mode. Use before launch or after a security scan.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: security
  source: https://hermes-ide.com/prompts/harden-web-app-config
  catalog: 2026.1004.2
---

# Harden web app headers and cookies

## Inputs

- [APP] (required): What the app is and how it is served - pages and APIs, auth method, inline scripts or styles, iframes, popups, subdomains, CDN or proxy.
- [FRAMEWORK] (optional): Where headers are set, e.g. "Express", "Next.js", "Django", "Rails", "nginx", "Cloudflare".
- [THIRD_PARTY_ORIGINS] (optional): External origins the app loads from or sends to - analytics, fonts, payment widgets, APIs, CDNs.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Security headers copied from a blog post either break the site on the first deploy (a CSP that blocks the payment widget, HSTS with preload on a domain whose subdomains are not all HTTPS) or are so loose they protect nothing (`unsafe-inline` everywhere, CORS reflecting any origin with credentials). Safe hardening means a policy fitted to how this app actually loads code and data, deployed in report-only mode first, then enforced.
</context>

<task>
Produce hardened header, CORS and cookie settings for:
[APP]
Only if [THIRD_PARTY_ORIGINS] was provided: 
Third-party origins in use:
[THIRD_PARTY_ORIGINS]
Only if [FRAMEWORK] was provided: 
Headers are set in: [FRAMEWORK]

1. If you do not know where headers are set, write the config for nginx and ask which layer the app uses.
2. Content Security Policy: prefer a strict policy with nonces or hashes and `'strict-dynamic'`, plus `object-src 'none'`, `base-uri 'none'` (or `'self'`), and `frame-ancestors`. Fall back to an allowlist only where a nonce is impossible, and say why. Include a reporting endpoint. Deploy it first as `Content-Security-Policy-Report-Only`.
3. HSTS: start with a short `max-age`, raise it to at least one year after checking, add `includeSubDomains` only once every subdomain serves HTTPS, and treat `preload` as a separate, deliberate decision that is hard to reverse.
4. Other headers: `X-Content-Type-Options: nosniff`, `Referrer-Policy: strict-origin-when-cross-origin`, a `Permissions-Policy` that disables features the app does not use, `Cross-Origin-Opener-Policy: same-origin` (check OAuth and payment popups first), and `X-Frame-Options: DENY` as a fallback for old browsers. Do not set the deprecated `X-XSS-Protection` filter.
5. CORS: only for endpoints that need cross-origin access; an explicit origin allowlist; never reflect the request origin or use `*` together with credentials; `Vary: Origin`; minimal allowed methods and headers.
6. Cookies: `Secure`, `HttpOnly` for anything scripts do not read, `SameSite=Lax` by default (`Strict` for sensitive actions, `None` only with `Secure` and a real cross-site need), the `__Host-` prefix for session cookies, and no `Domain` attribute unless subdomains must share it.
</task>

<constraints>
- Fit the policy to the third-party origins given. If an origin's needs are unclear, leave it out of the enforced policy and let report-only mode reveal it.
- Never recommend `'unsafe-inline'` or `'unsafe-eval'` for scripts without stating the risk and a plan to remove it.
- Write config only for the stated framework or server; do not invent middleware names you are unsure exist.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
</constraints>

<output_format>
## Policy
A table: header or setting, value, why, rollout stage (report-only, ramp, enforce).
## Config
Fenced code for the framework or server.
## Rollout
Numbered stages with durations and the signal to move to the next stage.
## Breakage to watch
Features likely to break (inline handlers, popups, embeds, widgets) and how to tell from violation reports.
## Verify
How to check the live headers and read the CSP reports.
</output_format>
