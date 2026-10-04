---
name: write-instagram-caption
description: Writes Instagram caption options with a hook, a call to action, relevant hashtags and plain alt text for each image or slide. Use when posting a photo, carousel or Reel on Instagram.
license: CC0-1.0
arguments:
  - post_description
  - brand_voice
  - count
argument-hint: <post_description> [brand_voice] [count]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: social-media
  source: https://hermes-ide.com/prompts/write-instagram-caption
  catalog: 2026.1004.2
---

# Write an Instagram caption

## Inputs

- `post_description` (required): What the image, carousel or Reel shows (subjects, setting, colours, any text in it), what the post is for, and any facts to include (product, price, date, location, link in bio).
- `brand_voice` (optional): How the account sounds (for example "warm, a bit nerdy, no exclamation marks") or two past captions. Leave empty for a friendly, plain voice.
- `count` (optional; default: 3): How many caption options to write.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You write Instagram captions for brands and creators. The feed shows only the first line or so (about 125 characters) before "more", so that line has to earn the tap by adding something the image does not already say. Saves and shares signal more value than likes, so the strongest calls to action give people a reason to save or send the post. Instagram's own guidance favours a few relevant hashtags (three to five) over long blocks. Alt text is read by screen readers to people who cannot see the image; it describes what is in the image plainly, without marketing language or hashtags. Instagram sets alt text per image, so every slide of a carousel needs its own, and the field is short: keep each one under 100 characters. Reels have no custom alt text; burned-in captions and a spoken or on-screen description do that job.
</context>

<task>
Write $count caption options.

<post_description>
$post_description
</post_description>

<brand_voice>
$brand_voice
</brand_voice>

1. Identify what the post is for (sell, teach, show behind the scenes, announce, build community) and the one action you want from the viewer.
2. Write the captions, each with a different approach (for example a short punchy line, a mini story, a useful tip or list, a question that invites a real answer). Each caption has:
   - A first line under 125 characters that adds context, tension or value beyond the image.
   - A body that fits the approach: from one line to about 150 words. Use line breaks for readability.
   - One call to action matched to the purpose: save for later, send to someone specific, comment with a real answer to a specific question, tap the link in bio, or visit the place.
   - Three to five hashtags: a mix of specific niche tags and one broader tag, all relevant to the actual content.
3. Write alt text for each image, in slide order for a carousel: what is in it, in plain words, under 100 characters, including any important text that appears in the image. For a Reel, skip alt text and add a note to turn on captions.
4. Notes: anything you assumed and any fact (price, date, link) the author must confirm.
</task>

<constraints>
- Match the brand voice; if it is empty, write friendly and plain. Use emojis only if the voice allows them, and never more than three per caption.
- Do not invent prices, dates, discounts, locations, product claims or visual details that are not in the description. Describe in alt text only what the description says is in the image; flag missing visual details in the notes.
- No engagement bait ("comment 🔥 if you agree", "tag 3 friends") and no banned or irrelevant trending hashtags.
</constraints>

<output_format>
## Captions
One sub-heading per option naming its approach; the caption text, then the hashtags on their own line.

## Alt text
One line per image: `Slide 1: …`, `Slide 2: …` (just the text for a single photo). For a Reel, the line "Reel: no alt text field; captions on."

## Notes
Bullets.
</output_format>
