<context>
You write transactional messages for appointment businesses. Reminders reduce no-shows when they arrive at the right time, say exactly when and where, make confirming or rescheduling one tap or one reply, and state the policy once without sounding like a threat. SMS must fit in one segment so it is cheap and arrives whole; email can carry the detail. Follow-ups after a missed appointment should keep the client, not punish them, and in health or care settings a missed visit can mean the person needs a call.
</context>

<task>
Write the appointment message set for a [BUSINESS_TYPE].

1. Define the merge fields you use, in square brackets so they are easy to map to any booking tool's own fields, each with the length you assume when counting characters: [FirstName] 8, [Date] 10 ("Tue 14 May"), [Time] 5 ("14:30"), [StaffName] 8, [BusinessName] 15, [Location] 20, [Link] 23 (a shortened link), [Phone] 13. If the real business name is longer than 15 characters, count it at its real length or suggest a short sender name.
2. Write each message in an SMS version (at most 160 characters with every merge field counted at its assumed length, with the count shown) and an email version (subject line plus a short body):
   - Booking confirmation
   - Reminder a few days before (adjust to the typical booking lead time)
   - Reminder the day before, with one-tap or reply-to-confirm
   - Reschedule or cancellation confirmed
   - Late cancellation, if a fee applies
   - No-show follow-up, first time (kind, offers rebooking)
   - No-show follow-up, repeat (states the policy plainly)
   - Waitlist offer when a slot opens
3. State the policy once, in the confirmation, and refer to it briefly elsewhere. If policies are empty, use `[POLICY: …]` placeholders.
4. Give a sending schedule and the opt-out or "reply STOP" note where marketing rules may require it.
</task>

<constraints>
- SMS versions must not exceed 160 characters; show the count for each, computed with the merge field lengths from step 1, and recount after any edit. Use only plain characters: no emoji, and straight quotes and apostrophes rather than curly ones, because one such character switches the whole message to the 70-character encoding. Symbols such as € and ~ cost two characters each in the standard encoding.
- Do not invent fees, notice periods, addresses or links; use placeholders.
- Never include health details, the reason for the appointment or anything sensitive in an SMS or email subject; a message on a lock screen can be read by others.
- One clear action per message. No guilt-tripping in no-show messages.
- Match the brand voice if given; otherwise warm, brief and professional.
</constraints>

<output_format>
## Merge fields
One line listing them.
## Message set
For each message: heading, then **SMS** (text and character count) and **Email** (subject and body).
## Sending schedule
Table: Message | Trigger or timing | Channel.
## Notes
Bullets: placeholders to fill, compliance points to check (consent for SMS, opt-out wording), and the health or care follow-up note if relevant.
</output_format>
