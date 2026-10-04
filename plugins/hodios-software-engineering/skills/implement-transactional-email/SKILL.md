---
name: implement-transactional-email
description: Implements transactional email with templates, a provider integration, retries, bounce and complaint handling, and deliverability settings. Use when an app must send receipts, resets or alerts.
license: CC0-1.0
arguments:
  - stack
  - emails_needed
argument-hint: <stack> [emails_needed]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: implementation
  source: https://hermes-ide.com/prompts/implement-transactional-email
  catalog: 2026.1004.2
---

# Implement transactional email

## Inputs

- `stack` (required): Language, framework, database, job queue if any, and the email provider if already chosen (for example Amazon SES, Postmark, SendGrid, Resend, Mailgun).
- `emails_needed` (optional): The emails to send, with trigger, recipient and content, for example "password reset, order receipt, weekly digest".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Transactional email fails silently: a reset link that lands in spam, a receipt sent twice because a request retried, an email sent for an order whose transaction then rolled back, a provider outage that drops messages, or a bounced address the app keeps mailing until the provider suspends the account. Since 2024, large mailbox providers require SPF, DKIM and a DMARC policy for bulk senders, alignment between the visible From domain and the signing domain, and one-click unsubscribe for marketing mail. Transactional and marketing mail belong on separate streams or subdomains so one cannot damage the other's reputation.
</context>

<task>
Implement transactional email for:
<stack>
$stack
</stack>
Only if emails_needed was provided: 
Emails needed:
<emails_needed>
$emails_needed
</emails_needed>

1. If the stack is unclear, ask once and stop. Read existing mail, job and config code if you can.
2. **Design.** Send from a background job, never inside the web request. Enqueue the email in the same database transaction as the business change (an outbox table, or the job system's transactional enqueue) so no email is sent for a rolled-back change and none is lost. Give each message an idempotency key derived from the event (for example `order-receipt:<order_id>`) and skip duplicates. Wrap the provider behind a small interface so tests use a fake and the provider can change.
3. **Templates.** One template per email with HTML and plain-text parts, variables escaped, a clear subject, the sender name, and localisation hooks if the app is multilingual. Keep secrets and long-lived tokens out of URLs except single-use, expiring tokens (password reset, magic link) that are invalidated on use.
4. **Sending and retries.** Use the provider's official SDK or HTTP API. Retry transient failures (timeouts, 429, 5xx) with exponential backoff and jitter up to a limit, then mark the message failed and alert. Do not retry permanent failures (invalid address, suppressed recipient). Log message id, template, recipient hash and status, never the full body of sensitive emails.
5. **Bounces and complaints.** Handle the provider's bounce, complaint and delivery webhooks with signature verification. Hard bounces and complaints add the address to a suppression list checked before sending; soft bounces are retried by the provider. Show a "we could not reach your email" state where it matters (password reset).
6. **Deliverability setup.** List the DNS records to create (SPF include, DKIM keys, DMARC starting at `p=none` with reporting and a plan to move to `quarantine` or `reject`, a custom return-path domain for alignment), a dedicated sending subdomain for transactional mail, and when a marketing stream needs one-click unsubscribe headers.
7. **Tests.** Unit tests with the fake provider for rendering, idempotency and suppression; a test that no email is sent when the transaction rolls back; and a local mail catcher for manual checks.
</task>

<constraints>
- Use the provider's documented API; if unsure of a method, header or webhook field for the version in use, say so rather than guessing.
- Do not invent DNS values, API keys or domains; use placeholders such as `mail.example.com`.
- Never send marketing content through the transactional stream.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Design
Bullets plus a short sequence of the send flow.
## Templates
One template in full as an example, then a table of the others with subject and variables.
## Code
Code blocks with file paths: interface, provider adapter, job, outbox or enqueue.
## Bounces and complaints
Webhook handler code and suppression logic.
## Deliverability setup
A table of DNS records with placeholder values and purpose.
## Tests
Code blocks with file paths, then the real result of running them, or a plain statement that they were not run.
## Open questions
Numbered, or "None".
</output_format>
