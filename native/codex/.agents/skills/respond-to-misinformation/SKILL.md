---
name: respond-to-misinformation
description: Helps reply to a friend or relative who shared misinformation, with what is wrong, the core fact, a non-judgemental message and a credible source to share. For people in family group chats.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: fact-checking
  source: https://hermes-ide.com/prompts/respond-to-misinformation
  catalog: 2026.1003.1
---

# Reply to someone sharing misinformation

## Inputs

- [CLAIM] (required): What was shared, pasted as-is (the message, post text or a description of the video), and where (family WhatsApp group, private message, Facebook).
- [RELATIONSHIP] (optional): Who shared it and what matters to them, for example "my dad, 70, worried about his health, trusts his doctor" or "a close friend who distrusts the government".
- [CHANNEL] (optional; one of: private, group; default: private): Whether to reply in the group or privately.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Corrections work best when they come from someone the person trusts, respect their underlying worry, and lead with the accurate information rather than the myth. The "truth sandwich" (fact first, then a brief mention of the myth and why it is misleading, then the fact again) avoids amplifying the false claim. Public mockery, long lectures and piles of links usually entrench the belief and damage the relationship. A private message is usually better than a correction in front of the group, but a short, neutral note in the group can protect others who saw the post. Many people share misinformation out of care ("I wanted you to be safe"), so the reply should honour that.
</context>

<task>
Help me reply about this:
<shared>
[CLAIM]
</shared>
Only if [RELATIONSHIP] was provided: Who shared it: [RELATIONSHIP]
Reply channel: [CHANNEL]

1. **What is wrong:** in two or three sentences, what is false or misleading, and the type of problem (made up, real but out of context, old news recirculated, exaggerated, a scam). Note anything in it that is true.
2. **The core fact:** the one accurate statement that replaces the myth, in plain words.
3. **Your message:** write a short, warm [CHANNEL] message in my voice, under about 80 words for a chat. Open with connection or shared concern, give the core fact, mention the myth only briefly, and end with an open question or offer rather than a verdict. If channel is group, keep it neutral and brief and suggest also messaging the person privately. Offer a second, even shorter version.
4. **A source to share:** suggest one credible, accessible source of the kind this person is likely to trust (a national health service, a well-known fact-checking organisation, a respected local outlet, the original source in context).
5. **If they push back:** two or three calm replies for likely responses ("I just shared it in case", "you can't trust them either"), and when to let it go.
</task>

<constraints>
- Do not invent facts, statistics or links. If you can browse, link only pages you opened. If you cannot, name the organisation and what to search for on its site, and tell me to check the page before sharing it.
- If you are not sure the claim is false, say so, and write a message that asks questions instead of correcting.
- Never mock or shame the person, and do not suggest tactics that could humiliate them in the group.
- If the shared content involves a health risk (for example stopping medicine or a dangerous remedy), make the core fact clear and suggest they talk to their doctor or pharmacist.
- If the content is a scam (asking for money, codes or personal details), say so first and include a warning not to click or pay.
- Stay neutral on politics; correct the fact, not the person's views.
</constraints>

<output_format>
Use the contract's section headings. Put the main and short versions of your message in quote blocks. Give the pushback replies as a two-column table: they say | you could reply.
</output_format>
