---
name: write-community-guidelines
description: Writes guidelines for a Discord server, forum, group or comment section with a purpose, clear rules with examples, moderation steps and an appeals route. Use when setting up or fixing a community.
license: CC0-1.0
arguments:
  - community
  - problems_seen
  - platform
argument-hint: <community> [problems_seen] [platform]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: social-media
  source: https://hermes-ide.com/prompts/write-community-guidelines
  catalog: 2026.1003.1
---

# Write community guidelines

## Inputs

- `community` (required): What the community is, who it is for, its size, what members do there, and the tone you want.
- `problems_seen` (optional): Problems you have had or expect, for example spam, self-promotion, heated arguments, off-topic posts, harassment, or members asking for free work.
- `platform` (optional): Where it lives, for example "Discord", "Reddit", "Facebook group", "Discourse forum", "YouTube comments".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a community manager who has built and moderated online communities from small servers to large forums. Good guidelines are short enough to be read, specific enough to be enforced, and explain the purpose behind the rules so members can judge cases the rules did not foresee. Long lists of vague prohibitions ("be nice", "no drama") are ignored and enforced inconsistently, which feels unfair. Members accept moderation when the rules are clear, examples show where the line is, the consequences are predictable, and there is a fair way to appeal.
</context>

<task>
<community>
$community
</community>

<problems_seen>
$problems_seen
</problems_seen>

Platform: $platform

1. **Purpose.** Two or three sentences: who the community is for, what it is for, and the kind of place it aims to be. Everything else follows from this.
2. **Rules.** Between five and ten, each written as a behaviour (what to do or not do), with a one-line reason and short examples of what is fine and what is not. Cover the problems listed; add others only when they are common for this kind of community. Always include: respect and no harassment or hate; no sharing others' private information; spam and self-promotion limits; staying on topic with a place for off-topic; and following the platform's own terms. Order the rules by how often they will matter.
3. **Enforcement ladder.** What happens on a first, second and third breach (for example a reminder, a warning, a temporary mute or suspension, a ban), and which behaviours skip the ladder and lead to immediate removal (threats, doxxing, hate speech, sexual content involving minors, illegal content). For content that endangers someone or sexualises minors, moderators also report it to the platform's trust and safety team and, where the law requires or someone is at risk, to the authorities; they report it through the platform's tools and never download, save or re-share it. Say how members report problems.
4. **Appeals.** How a member appeals, to whom, within what time, and that a different moderator reviews it where possible.
5. **Moderator conduct.** How moderators act: consistently, transparently, without using moderation in personal disputes, with a log of actions.
6. **Short version.** A condensed version that fits a sidebar, channel topic, pinned comment or rules-screening form on $platform, using that platform's features where relevant.
7. **Templates.** Short, neutral messages for a reminder, a warning, a removal with reason, and an appeal outcome.
</task>

<constraints>
- Plain language, second person, positive framing where it does not blur the rule ("Keep promotion to the #showcase channel" rather than "No promotion").
- Do not present the guidelines as legal advice or as replacing the platform's terms or the law; for communities with minors, health, finance or legal topics, add a line telling members the community does not give professional advice and suggest the owner checks relevant obligations.
- If the platform is not given, write platform-neutral guidelines and note where features differ.
- Do not invent community history, member counts or incidents.
- Keep the full guidelines under about 600 words; brevity is what gets them read.
</constraints>

<output_format>
## Guidelines
The full text, ready to publish: purpose, numbered rules with examples, enforcement, reporting, appeals.

## Short version
Ready to paste into $platform.

## Moderation playbook
A table: behaviour | first time | second time | third time | notes. Then moderator conduct.

## Message templates
Four short templates.

## Before you publish
Decisions the owner must make (moderators, appeal contact, channels to create) and settings to configure on the platform.
</output_format>
