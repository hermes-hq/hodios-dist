---
description: Implements a payment integration with the provider's official SDK, covering checkout, webhooks, idempotency, refunds and reconciliation. Use when adding one-time payments or subscriptions.
agent: agent
argument-hint: stack provider billing_model
---

# Integrate payments

<context>
Payment bugs cost money or trust: double charges from retried requests, orders marked paid because the browser hit a success URL, fulfilment that never happens because a webhook was missed, refunds recorded locally but not at the provider, and amounts in floating point. The provider is the source of truth for payment state; the app learns about it from verified webhooks, processes each event idempotently and reconciles daily. Hosted checkout pages or provider UI elements keep card data off the app's servers and reduce PCI DSS scope to the simplest self-assessment level.
</context>

<task>
Implement a ${input:billing_model:One-time purchases or recurring subscriptions.} payment integration for:
<stack>
${input:stack:Language, framework, database, and how orders or accounts are modelled today.}
</stack>
Only if provider was provided (leave it empty to skip): 
Provider: ${input:provider:Payment provider, for example Stripe, Adyen, PayPal, Mollie, Paddle or Braintree.}

1. If the provider or stack is missing, ask once and stop. Read the existing order, account and user models if you can.
2. **Design.** Use the provider's hosted checkout or embedded UI components, never raw card fields. Model payment state in the app as a small state machine (for one-time: pending, paid, failed, refunded or partially refunded; for subscriptions: trialing, active, past due, canceled, plus the provider's customer and subscription ids). Store amounts as integer minor units with an ISO 4217 currency code, and compute prices on the server, never from the client.
3. **Checkout.** Server endpoint that creates the checkout or payment intent with the official SDK, sends an idempotency key derived from the order or request, attaches the app's order or user id as metadata, and returns what the client needs. The success redirect only shows a "processing" or confirmation page; it never marks the order paid.
4. **Webhooks.** An endpoint that reads the raw body, verifies the signature with the provider's SDK and the webhook secret, rejects stale timestamps, stores the event id to skip duplicates, acknowledges quickly with a 2xx and does the work in a background job, tolerates out-of-order events by fetching the current object from the provider when order matters, and updates state through the state machine. List the event types to handle for ${input:billing_model:One-time purchases or recurring subscriptions.} (for subscriptions include payment failure and dunning, renewal, plan changes, cancellation and the end of a trial).
5. **Refunds and reconciliation.** Refunds go through the provider API with an idempotency key and are confirmed by webhook. A daily job compares the provider's balance transactions or payouts with the app's records and reports mismatches. Handle disputes and chargebacks as events.
6. **Tests.** Use the provider's test mode, test cards and its CLI or fixtures for sending signed test webhooks. Cover the happy path, a declined payment, a duplicate webhook, an out-of-order webhook, an invalid signature, a refund, and (for subscriptions) a failed renewal.
</task>

<constraints>
- Use the provider's official SDK and its current documented API. If you are unsure of a method, event name or field for the SDK version in use, say so and point to the docs rather than guessing.
- Never log full card data, payment method details or webhook secrets; never put secret keys in client code.
- Never use floating point for amounts, and never trust amounts, prices or currencies sent by the client.
- Taxes, invoicing rules and refund policy are business and legal decisions; ask, or leave a marked hook, rather than inventing them.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Design
State machine (Mermaid `stateDiagram-v2`), data model changes, and the end-to-end flow in numbered steps.
## Code
Code blocks with file paths for checkout and models.
## Webhooks
Code with file paths, then a table of event types and the state transition each causes.
## Refunds and reconciliation
Code or job outline.
## Tests
Code with file paths, then the real result of running them, or a plain statement that they were not run.
## Go-live checklist
Checkboxes: live keys in the secrets store, webhook endpoint registered in live mode, idempotency verified, alerts on webhook failures, reconciliation job scheduled, refund policy confirmed.
## Open questions
Numbered.
</output_format>
