---
name: write-self-introduction
description: Writes a short self-introduction for a new team, class, community or meeting round in 15-second, 60-second and written forms, built around one memorable detail.
license: CC0-1.0
arguments:
  - about_you
  - setting
argument-hint: <about_you> <setting>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: interpersonal-communication
  source: https://hermes-ide.com/prompts/write-self-introduction
  catalog: 2026.1004.1
---

# Write a self-introduction

## Inputs

- `about_you` (required): Your name, what you do or study, what brings you here, and a few true things about you outside work (hobbies, where you are from, an odd skill, something you are learning).
- `setting` (required): Where you will introduce yourself, for example "first day on a new marketing team", "evening pottery class", "open-source project Discord" or "round of intros at a 40-person conference workshop".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Introductions go wrong in the same ways: a job title and nothing else, a CV recital, or a nervous joke. What people remember about a new person is one concrete, slightly unexpected detail and a sense of why they are here and what they are like to talk to. The setting decides what is relevant: a new team wants your role and how to work with you; a class wants why you joined; a community wants what you are interested in and can offer. A good introduction ends with an opening, something people can come up to you about later.
</context>

<task>
Write my self-introduction for: $setting

<about_you>
$about_you
</about_you>

1. If the details are missing what the setting needs most (for example a new team needs my role), ask for it in one question and stop.
2. Choose what is relevant for this setting and this audience, and leave out the rest.
3. Choose one memorable detail from my details: concrete, true, and easy to ask about. Prefer something people can relate to or follow up on over a boast.
4. Write three versions: 15 seconds spoken, 60 seconds spoken, and written (for a chat channel, forum or welcome thread).
5. Give three conversation hooks: things people could ask me about afterwards, and one question I could ask the group.
</task>

<constraints>
- Spoken versions: about 30 to 40 words for 15 seconds and 120 to 150 words for 60 seconds (people speak about 130 to 150 words a minute when introducing themselves), written for the ear in short sentences, with my name early and again at the end of the 60-second version only if the room is large.
- Written version: 50 to 90 words, friendly, one or two line breaks, no hashtags, and an emoji only if the setting is casual.
- Use only facts I gave. Do not invent hobbies, achievements, numbers or jokes.
- Match the setting's register: a board meeting is not a pottery class.
- No humblebrags, no "I'm passionate about…", no list of more than three things.
- End each version with an opening: what I would love to talk about, learn or help with.
</constraints>

<output_format>
## 15 seconds
The words, then the word count in brackets.
## 60 seconds
The words, then the word count in brackets.
## Written
The post or message.
## The memorable detail
One line on which detail you chose and why it works here.
## Conversation hooks
Three bullets.
</output_format>
