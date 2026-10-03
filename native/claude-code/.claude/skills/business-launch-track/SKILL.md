---
name: business-launch-track
description: Takes a validated business idea to launch in gated steps - offer and pricing, a legal and admin checklist to verify, setup, launch marketing and a first-90-days review.
license: CC0-1.0
arguments:
  - validated_idea
  - country
  - budget
argument-hint: <validated_idea> [country] [budget]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: entrepreneurship
  source: https://hermes-ide.com/prompts/business-launch-track
  catalog: 2026.1003.2
---

# Business launch track

## Inputs

- `validated_idea` (required): The idea and the evidence that it is validated - who the customer is, what they said or paid, the offer you tested and the results. Paste your validation notes if you have them.
- `country` (optional): Country (and region if rules differ) where you will register and trade. Used only to frame checks to verify, never to state rules.
- `budget` (optional): Money and weekly hours available until launch and for the first three months (for example "2,000 and 15 hours a week"). If empty, the track assumes a lean launch and says so.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Takes a validated idea to a business that is open and selling, then reviews it after 90 days. Each step stops for approval; step 5 waits for real numbers.

<validated_idea>
$validated_idea
</validated_idea>
Only if country was provided: 
Country: $country
Only if budget was provided: 
Budget and time: $budget

Rules for every step:
- If the validation evidence rests on opinions rather than commitments (pre-orders, deposits, paid pilots), say so, suggest validating first, and continue only if the founder confirms.
- Launch the smallest version customers will pay for.
- Never invent prices, competitor facts, costs or legal requirements. Registration, tax, licences, insurance, data protection and consumer law are checks to verify with official sources, an accountant or a lawyer. Keep a running assumptions list.
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- If no budget is given, assume a lean launch (a few hundred in spend, evenings and weekends) and say so.
- Keep a launch checklist with owner and due date, reprinted at the end of each step.

## Steps

Work through these steps in order. Do not skip a gate.

1. offer (plan)
2. legal-admin (plan)
3. setup (build)
4. launch (ship)
5. first-90-days (review)

### Step 1: Offer and pricing

1. Evidence check: summarise what the validation proved and what it did not, in a table (Assumption | Evidence | Strength). Name the riskiest assumption still open.
2. Launch offer: what is sold, to whom, the promised outcome, what is included and excluded, how it is delivered, and the guarantee or refund terms. One core offer; at most one entry option and one premium option.
3. Pricing: build the price from three angles and show each - cost floor (direct cost per sale plus a share of monthly fixed costs at a realistic volume), what customers paid or committed to in validation, and the alternatives customers use today. Recommend a launch price; any launch discount needs an end date. Never price below the cost floor without saying so.
4. Unit economics: margin per sale, and monthly sales needed to cover fixed costs and to pay the founder a stated minimum income. Show the sums.
5. Positioning line: "For <customer> who <need>, <offer> gives <outcome>, unlike <alternative>."
6. Later list: features and ideas deliberately left out of the launch.

Output each item above, in order.

Stop for approval of the offer and price before step 2.

**Gate:** stop here and wait for the user's approval before step 2 (legal-admin).

### Step 2: Legal and admin checklist to verify

1. Structure: the options commonly available (sole trader, partnership, limited company or LLC) and what decides between them - liability, tax, admin. Recommend an accountant for the choice.
2. Registration and tax: business and tax registration, sales tax or VAT thresholds, record-keeping, payment dates, setting money aside for tax from the first sale.
3. Sector permissions: licences, permits or qualifications that may apply (food, alcohol, childcare, health, finance, trades, home-based work, premises use).
4. Insurance to ask a broker about: public, product and professional liability, employer's liability if hiring, equipment, cyber.
5. Customer terms: terms of sale, refunds and cancellations, consumer rights for online sales, privacy notice, marketing consent.
6. Name: company register, trademark, domain and social handle checks.
7. Money: business bank account, payment provider, invoicing and bookkeeping.

Output a table: Item | Applies because | What to verify | Who to ask | Before launch? | Status. Mark items "check", never "not required".

Stop for approval. Ask the founder to complete the before-launch checks and report anything that changes the offer or budget.

**Gate:** stop here and wait for the user's approval before step 3 (setup).

### Step 3: Setup

1. Minimum operating setup for the approved offer: how customers find, buy, receive and get help - for example a one-page site or shop listing, a booking or checkout tool, payment, delivery or fulfilment, an inbox, and a simple way to record sales and costs. Choose the simplest tools that work; name tool types, not brands, unless the founder already uses one.
2. Delivery process: a short checklist from order to delivered, including what happens when something goes wrong (late, faulty, refund request).
3. Budget: a table of one-off and monthly setup costs within the stated budget, with what to skip if money is tight.
4. Readiness test: a dry run in which a friend completes the whole journey, from finding the offer to paying, receiving it and asking for help.
5. Timeline: tasks to launch day, by week, within the founder's weekly hours.

Output the setup table (Need | Simplest option | Cost | Owner | Done by), the delivery checklist, the budget table, the readiness test and the timeline.

Stop for approval, then ask the founder to run the readiness test and report what broke.

**Gate:** stop here and wait for the user's approval before step 4 (launch).

### Step 4: Launch marketing

If the step 3 readiness test has not been run, ask for its results first.

1. Launch target: paying customers for the first 30 days, derived from step 1's unit economics, plus weekly leading indicators (visits, enquiries, conversion).
2. Warm launch: validation contacts, waitlist, pre-order customers and the founder's network, with a personal message for each group.
3. Channels: the two or three channels most likely to reach this customer on this budget, ranked, with weekly actions; say why others wait.
4. Assets: announcement post or email, listing description, and a referral ask, built on the positioning line.
5. Launch week: day by day, with owner and time.
6. Tracking sheet: Date | Channel | Action | Contacts | Enquiries | Sales | Revenue.

Keep copy claims to what the offer delivers.

Stop for approval. Ask the founder to launch and return at 90 days (earlier if the 30-day target is badly missed) with the tracking sheet, sales and costs.

**Gate:** stop here and wait for the user's approval before step 5 (first-90-days).

### Step 5: First-90-days review

Without real numbers (sales, revenue, costs, the tracking sheet, customer feedback), ask for them and stop; never estimate or simulate results.

1. Scorecard: targets set in steps 1 and 4 against actuals - customers, revenue, margin, founder hours, cash left. Show the gap.
2. Funnel: where people dropped out (never found it, found but did not buy, bought only once) and which channel produced paying customers, not just attention.
3. Customers: what the first customers said, why they bought, complaints and refund reasons, and who the best customers turned out to be.
4. Operations: what took longer or cost more than planned, and the checklist items from step 2 still open.
5. Decision: recommend one, with the reasoning - double down (what to do more of), adjust (offer, price, customer or channel, with the next test), or pause or stop (say so plainly and list what is reusable). Name the numbers that would change this decision.
6. Next 90 days: three priorities with measurable targets, what to stop doing, and the date of the next review.

Output each item above, in order. End with the single most important next action.
