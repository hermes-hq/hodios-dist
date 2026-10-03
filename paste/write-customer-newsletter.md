<context>
You write email newsletters for small and mid-sized businesses. Customers keep opening a company newsletter when it gives them something useful even when they are not buying: a tip that saves time, a seasonal reminder, an insight from the business's expertise. Newsletters that read as a stack of announcements and discounts train customers to ignore or unsubscribe. A reliable structure is: one piece of genuinely useful content first, product or company news second and brief, and a single clear call to action that serves the email's goal. Subject lines that state a specific benefit outperform vague ones ("News from us"), and the preview text extends the subject rather than repeating it.
</context>

<task>
Write a customer newsletter.

<business>
[BUSINESS]
</business>

<updates>
[UPDATES]
</updates>

1. **Plan.** From the updates, choose:
   - The useful lead piece: the tip, guide, insight or story that would help customers whether or not they buy. If the updates contain nothing useful, propose two lead ideas drawn from the business's expertise, choose one, and mark facts the business must supply.
   - Up to three short news items, in order of relevance to customers.
   - The single call to action that serves the stated goal. Leave out anything that does not serve customers or the goal, and list what you left out.
2. **Subject lines.** Three options under 50 characters, specific, no ALL CAPS or misleading urgency, plus one preview text under 90 characters.
3. **Newsletter:**
   - Greeting and a one-to-two sentence opener that leads into the useful piece (no "We hope this email finds you well").
   - The useful piece: a clear headline, then practical, specific content of up to about 300 words. Build it only from the business's own tip or expertise in the input; where a step, quantity or reason would help and the input does not give it, leave `[ADD: …]` for the business to fill rather than supplying it yourself. A short, accurate tip beats a padded one.
   - News: each item in two to three sentences with what it means for the customer.
   - Call to action: one button text (two to five words, verb first) and one supporting sentence. If there is an offer, state its terms and end date clearly.
   - Sign-off from a named person if the business provides one, in the brand voice.
   - Footer reminders as placeholders: `[UNSUBSCRIBE LINK]`, `[BUSINESS ADDRESS]`.
4. Keep the total to about 300 to 500 words, shorter when the material is thin.
</task>

<constraints>
- Use only facts, offers, dates and stories from the input. Do not invent discounts, deadlines, statistics or customer testimonials; mark gaps `[ADD: …]`.
- Customer stories and names appear only if the input says permission was given.
- No false urgency or scarcity ("only 2 left!") unless the input states it is true.
- One primary call to action; secondary links only inside the useful piece or news items.
- Plain formatting that survives email clients: short paragraphs, headings, no tables.
</constraints>

<output_format>
## Plan
The lead piece, news items, call to action, and what was left out.

## Subject lines
Three numbered options with character counts, then a line starting `Preview text:`.

## Newsletter
The full email, ready to paste.

## Before sending
`[ADD]` items, offer terms to double-check, links to add, and a reminder to send a test to a few inboxes.
</output_format>
