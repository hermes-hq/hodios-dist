---
name: website-copy-track
description: Writes a small-business website in gated steps, from customer research and messaging to sitemap, homepage, inner pages and a final clarity and claims review.
license: CC0-1.0
arguments:
  - business_description
  - customers
  - pages_needed
argument-hint: <business_description> [customers] [pages_needed]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: copywriting
  source: https://hermes-ide.com/prompts/website-copy-track
  catalog: 2026.1004.0
---

# Small-business website copy track

## Inputs

- `business_description` (required): What the business does, where, for whom, prices or packages, what makes it different, proof you have (reviews, years trading, accreditations), and the main action you want visitors to take (call, book, buy, request a quote).
- `customers` (optional): What you know about customers in their own words, such as reviews, common questions, enquiry emails, reasons they chose you or reasons they did not. Optional, but the copy is far stronger with it.
- `pages_needed` (optional): Pages you already know you want (for example "home, services, about, pricing, contact"). Optional; the sitemap step proposes them otherwise.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Writes a small-business website the way a senior web copywriter would: understand the customers, agree the message, plan the pages, then write the homepage, the inner pages and a final review, one approved step at a time.

<business_description>
$business_description
</business_description>

Only if customers was provided: <customers>
$customers
</customers>
Only if pages_needed was provided: Pages requested: $pages_needed

Each step produces one artifact and stops for approval or edits; later steps build on the approved versions and do not reopen them unasked. Use only facts the owner supplied: never invent reviews, client names, years in business, accreditations, prices or results. Ask for missing facts or mark them `[NEEDED: …]`. Write for visitors who arrive on any page from a search, so every page says what it is, who it is for and what to do next. If the owner asks to skip approvals, confirm once that later steps will build on unreviewed choices; if they agree, run the remaining steps in one reply and state the choice made at each skipped gate.

## Steps

Work through these steps in order. Do not skip a gate.

1. research (discover)
2. messaging (plan)
3. sitemap (plan)
4. homepage (build)
5. inner-pages (build)
6. review (review)

### Step 1: Customer research

Find out what customers want and how they say it, before writing a word of copy.

1. If the description does not say what the business sells, where it operates (or that it is online only) and what action visitors should take, ask for those in one message and stop.
2. From the customer material, pull exact phrases into a table: Theme | Customer words | Source. Cover the problem that brings them, the result they want, what they tried before, what made them choose this business, and what worried them before buying.
3. If there is little or no customer material, say so plainly, list the assumptions you would otherwise make, and give the owner five questions to ask three recent customers (or a way to mine reviews and enquiry emails). Offer to continue on labelled assumptions.
4. Name the two or three customer types the site must serve, by situation and need, not demographics (for example "landlord needing a gas safety certificate this week").
5. List the questions visitors ask most before getting in touch; these become page sections and FAQs later.

Stop and wait for approval or edits. Do not write messaging yet.

**Gate:** stop here and wait for the user's approval before step 2 (messaging).

### Step 2: Messaging

Agree what the site says before deciding where it says it.

1. Write a one-sentence positioning line: for [customer type] who [need], [business] is the [category] that [main benefit], unlike [main alternative] because [reason supported by a fact].
2. Write the core message: a headline-length promise and a two-sentence explanation, in the customers' words from step 1.
3. List three to four key messages (the reasons to choose this business), each with the proof the owner supplied or `[NEEDED: proof]`.
4. Define the voice in three adjectives with a "this, not that" example for each (for example "plain: 'we fix leaks', not 'we provide remedial plumbing solutions'").
5. Note the main objection for each customer type and the fact that answers it.
6. Name the primary call to action, worded as a verb plus what happens next, and one secondary action for visitors not ready yet.

Stop and wait for approval or edits. Do not plan pages yet.

**Gate:** stop here and wait for the user's approval before step 3 (sitemap).

### Step 3: Sitemap and page plan

Plan the fewest pages that answer what visitors need.

1. Start from the requested pages, if any, and the visitor questions from step 1. Propose a sitemap, usually five to eight pages: home, one page per main service or product group (so each can rank for its own searches), about, pricing if prices can be shown, a proof page if there is enough proof, and contact. Merge or cut thin pages.
2. Give each page a table row: Page | Main visitor and question it answers | Search phrase it should rank for (labelled as an assumption unless the owner supplied keywords) | Key sections | Primary call to action | Proof used.
3. Sketch the main navigation (at most six items) and the footer contents (contact details, opening hours, service area, legal pages).
4. List any page the owner requested that you suggest dropping or merging, with the reason.
5. List the facts still needed per page.

Stop and wait for approval or edits. Do not write the homepage yet.

**Gate:** stop here and wait for the user's approval before step 4 (homepage).

### Step 4: Homepage copy

Write the homepage from the approved messaging and page plan.

1. Hero: a headline of at most about 10 words saying what the business does and for whom (clarity beats cleverness), a subhead with the main benefit and area served, the call-to-action button (at most 5 words, starting with a verb), and one trust line (rating, years trading or accreditation, only if supplied).
2. Sections in this order, each with a heading that makes sense on its own when skimmed:
   - The problem or situation, in customers' words.
   - Services or products, one short card each linking to its page.
   - Why choose us: the key messages with their proof.
   - How it works: three steps from first contact to result.
   - Proof: reviews or results exactly as supplied, or `[NEEDED: …]` placeholders.
   - FAQ: three to five of the most common questions.
   - Closing call to action with contact details.
3. Write a page title (under about 60 characters) and a meta description (under about 155 characters) for the homepage.
4. Keep body copy scannable: paragraphs of at most three lines, about a grade 7-9 reading level, "you" more than "we".

Stop and wait for approval or edits. Do not write inner pages yet.

**Gate:** stop here and wait for the user's approval before step 5 (inner-pages).

### Step 5: Inner pages

Write every other page in the approved sitemap, consistent with the approved homepage.

For each page:

1. Page title (under about 60 characters) and meta description (under about 155 characters).
2. A headline that names the page's subject and its main benefit, and an opening paragraph that confirms to a visitor arriving from a search that they are in the right place.
3. The sections planned in step 3. Service pages: who it is for, what is included, how it works, pricing, proof, FAQ. About page: why the business exists and the people, shown through facts, not adjectives. Contact page: ways to get in touch, response time, service area and hours.
4. One primary call to action, repeated at the end of the page.
5. Two or three internal links to related pages, with descriptive link text.

After the pages, list every `[NEEDED: …]` placeholder in one place, grouped by page, so the owner can collect them in one go.

Stop and wait for approval or edits before the final review.

**Gate:** stop here and wait for the user's approval before step 6 (review).

### Step 6: Clarity and claims review

Review the whole site's approved copy as a first-time visitor and as a careful editor.

1. **Five-second test per page:** can a visitor tell what this is, who it is for and what to do next from the top of the page alone? Quote any page that fails and give the fix.
2. **Consistency:** the same names for services, prices, opening hours, service area, phone number and calls to action on every page. List every mismatch.
3. **Claims:** list every claim that needs proof or may be regulated ("guaranteed", "free", "cheapest", "best in town", health, financial or environmental claims, accreditations). For each: the page, the wording, whether proof was supplied, and a safer rewrite if not.
4. **Placeholders:** every remaining `[NEEDED: …]` item.
5. **Readability and accessibility:** long sentences, jargon, vague link text ("click here"), and images that will need alt text.
6. **Launch list:** the five most important fixes, in order, before the site goes live.

This is the last step.
