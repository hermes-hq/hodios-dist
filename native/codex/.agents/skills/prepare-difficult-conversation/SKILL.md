---
name: prepare-difficult-conversation
description: Prepares a difficult conversation with realistic goals, an opening line, the other person's likely view, phrases to use and responses to pushback, and points to help instead when safety is at risk.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: interpersonal-communication
  source: https://hermes-ide.com/prompts/prepare-difficult-conversation
  catalog: 2026.1004.2
---

# Prepare for a difficult conversation

## Inputs

- [SITUATION] (required): What the conversation is about, what has happened so far, and what worries you about raising it.
- [RELATIONSHIP] (optional): Optional: who the other person is to you, for example "my direct report", "my landlord", "my brother", "a co-founder".
- [DESIRED_OUTCOME] (optional): Optional: what you want to be true after the conversation, for example "she stops cc'ing my boss on everything" or "we agree a plan for Mum's care".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Difficult conversations go wrong in predictable ways: the person goes in to win rather than to solve, opens with an accusation or a long preamble, treats their own story about the other person's motives as fact, and has no plan for the moment the other person gets defensive. Preparation that helps is concrete: a clear purpose, a short neutral opening, genuine curiosity about the other side, and a few phrases ready for the hard moments. The aim is a better outcome and a relationship that survives, not a perfect script.
</context>

<task>
Help me prepare for this conversation:
<situation>
[SITUATION]
</situation>
Only if [RELATIONSHIP] was provided: The other person is: [RELATIONSHIP].
Only if [DESIRED_OUTCOME] was provided: What I want afterwards: [DESIRED_OUTCOME]

1. Safety first. If the situation involves violence, threats, coercive control, stalking or fear for anyone's safety, do not prepare a confrontation. Follow the safety guidance below and stop.
2. If the situation is too thin to know who the conversation is with or what it is about, ask up to three short questions and stop.
3. Goals: separate what I want for myself, for them and for the relationship. If no outcome was given, propose one. Check it is within my control (I can ask for a change; I cannot make them agree) and say what a realistic good result looks like.
4. Their likely view: write their side as they would tell it, as charitably as the facts allow, and list what they might be worried about. Separate what I actually observed from what I am assuming about their intentions.
5. Opening: two or three sentences I can say word for word that name the topic, my intent and an invitation to talk, without blame or a long build-up. Suggest the right time, place and medium.
6. Phrases that help: five to eight lines for describing facts and impact ("I" statements), asking questions, acknowledging their view without conceding the point, and proposing a next step.
7. If they push back: the four or five most likely reactions (denial, anger, tears, counter-accusation, silence, changing the subject) and a calm response to each.
8. What to avoid, and how to pause or end the conversation if it escalates.
9. After: how to confirm what was agreed and when to follow up.
</task>

<constraints>
- Fit everything to the relationship: what works with a direct report differs from a parent, a partner or a landlord. A manager has power the other person does not; account for it.
- Do not script manipulation, guilt-tripping, ultimatums I have not said I mean, or anything dishonest.
- If the situation involves workplace harassment, discrimination, a legal dispute or a tenancy or employment right, note once that HR, a union, a lawyer or an advice service may be the right route alongside or instead of the conversation.
- Keep each phrase short enough to say naturally.
- If the person mentions thoughts of suicide or self-harm, harming someone else, abuse, or being in danger, stop the exercise. Respond with care, tell them they deserve support now, and point them to local emergency services or a crisis line in their country. If you do not know their country, ask, and mention that local emergency numbers work everywhere.
- You are a supportive tool, not therapy. For ongoing distress, low mood that lasts, or anything that disrupts daily life, encourage them to talk to a doctor or a licensed mental-health professional.
- Never shame, diagnose, or tell someone what they "really" feel. Reflect back what they said and offer, rather than impose, next steps.
</constraints>

<output_format>
## Goals
For me, for them, for the relationship, and a realistic good outcome.
## Their likely view
Their side in their words, then "What I know" versus "What I'm assuming".
## Opening
The words to say, plus when and where.
## Phrases that help
Bullets.
## If they push back
A table: If they… | You can say…
## Avoid
Bullets, including how to pause the conversation.
## If it goes badly
How to end it well and what to do next.
## After
How to confirm agreements and follow up.
</output_format>
