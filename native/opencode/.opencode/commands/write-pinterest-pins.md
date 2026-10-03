---
description: Writes Pinterest pin titles, descriptions, board names and text-overlay ideas that match search intent for a product, recipe or article. Use when promoting content on Pinterest.
---

# Write Pinterest pins

## Inputs

- [CONTENT_OR_PRODUCT] (required): The product, recipe, article or page the pins link to, with its key details, who it is for, the destination URL, and any seasonal timing.
- [KEYWORDS] (optional): Search terms you have found in Pinterest's search bar suggestions or Pinterest Trends, if any.
- [PIN_COUNT] (optional; default: 5): How many distinct pins to write.

Read each value from the arguments below. If a required value is missing, ask for it once.

<context>
You write Pinterest pins. Pinterest behaves like a visual search engine more than a social feed: people come to plan (dinners, outfits, rooms, trips, projects), they search with descriptive phrases, and they save pins to boards for later. A pin is found through the keywords in its title, description, board and the image itself, and it can keep bringing traffic for months. Pins that work show the outcome in a tall image (2:3 ratio is standard), carry a short text overlay that says what the click delivers, and use natural, descriptive language rather than hashtags. Only the start of a title shows in the feed, so the most important words go first. People search for seasonal ideas well ahead of the date, often a month or more.
</context>

<task>
Write [PIN_COUNT] distinct pins for this content.

<content>
[CONTENT_OR_PRODUCT]
</content>

<keywords>
[KEYWORDS]
</keywords>

1. **Search intent.** Name the two or three things a Pinner would be planning or trying to solve when this content is the answer, and the descriptive phrases they would type. Use the supplied keywords first; add natural variations and mark them as suggestions to verify.
2. **Pins.** Write [PIN_COUNT] pins, each aimed at a different intent or angle (for example the outcome, a how-to, a list, a specific use case, a seasonal angle). For each pin:
   - Title: up to 100 characters, the main phrase in the first 40.
   - Description: two to three natural sentences, up to 500 characters, with the main and one or two related phrases, what the click delivers, and a soft call to action (save it, try it, shop it).
   - Text overlay: at most six words, readable on a phone.
   - Image concept: what the 2:3 image shows and where the overlay sits.
   - Alt text: a plain description of the image.
   - Board: which board it belongs on.
3. **Board names.** Three to five keyword-rich board names with a one-line board description each.
4. **Keyword checks.** How to confirm the phrases using Pinterest's search suggestions and Trends, and when to publish if the content is seasonal.
</task>

<constraints>
- Describe the content accurately: no claims, prices, results or features that are not in the material. Use `[FILL: …]` where a detail is missing.
- Do not state search volumes or trend data; you have not seen them.
- No hashtags, emoji strings or clickbait. Each pin must be distinct, not the same words reshuffled.
- If the content is a product with an affiliate or paid relationship, add a disclosure note to the description.
</constraints>

<output_format>
## Search intent
Bullets.

## Pins
One numbered block per pin with the six fields above.

## Board names
A list with descriptions.

## Keyword checks
Bullets, including the suggested publish timing.
</output_format>

Arguments: $ARGUMENTS
