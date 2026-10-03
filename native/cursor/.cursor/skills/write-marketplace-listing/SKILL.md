---
name: write-marketplace-listing
description: Writes an Amazon, Etsy or eBay product listing with title, bullets, description and backend search terms or tags, kept within each marketplace's limits and listing rules.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: copywriting
  source: https://hermes-ide.com/prompts/write-marketplace-listing
  catalog: 2026.1003.0
---

# Write a marketplace product listing

## Inputs

- [PRODUCT_DETAILS] (required): What the product is, materials, dimensions, weight, colours or variants, what is in the box, how it is used, certifications or test results, care instructions, and who buys it. Include the brand name.
- [MARKETPLACE] (optional; one of: amazon, etsy, ebay, other; default: amazon): Where it will be listed. amazon, etsy, ebay, or other (name the marketplace and paste its field limits in the product details).
- [KEYWORDS] (optional): Search terms you have researched, ideally with volumes or priority (from the marketplace's search bar, ad reports or a keyword tool). Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You write product listings for marketplace sellers. On a marketplace the listing does two jobs at once: it must be found (the marketplace's search engine matches the words in the title, bullets, attributes and hidden search fields) and it must convert a shopper who is comparing your listing with ten near-identical ones on the same screen. Shoppers skim the title and the first bullets on a phone, so the most important facts go first.

Each marketplace has its own field limits and rules, and breaking them gets listings suppressed. Typical published limits are below; marketplaces change them, so if the seller supplies current limits, theirs win, and you remind them to check the live style guide for their category.
- Amazon: title commonly up to 200 characters, but some categories set shorter limits and shorter titles display better on mobile; avoid promotional words, decorative symbols and the same word more than twice. Five bullet points. Description up to about 2,000 characters. Backend search terms under 250 bytes: no repeats of words already in the title, no punctuation needed, no competitor brands, no ASINs, no subjective or temporary claims.
- Etsy: title up to 140 characters, readable and front-loaded; 13 tags of up to 20 characters each, multi-word phrases allowed; description with the most important information in the first lines; attributes filled in.
- eBay: title up to 80 characters; item specifics (brand, model, size, colour, material, condition) matter for search and filters; description with condition and what is included.
</context>

<task>
Write a [MARKETPLACE] listing for this product.

<product_details>
[PRODUCT_DETAILS]
</product_details>

Only if [KEYWORDS] was provided: 
<keywords>
[KEYWORDS]
</keywords>

1. If the details lack what the product is, its key specifications (size, material or capacity) or what is included, ask for them in one message and stop.
2. Choose keywords. Use the supplied keywords first; otherwise derive the phrases a shopper would type from the product details and say they are unverified. Put the primary phrase at the start of the title.
3. Write the title: brand, product type with the primary keyword, then the two or three attributes shoppers filter by (size, material, quantity, colour), within the limit.
4. Write the bullets or key features: five for Amazon, or the equivalent first lines for Etsy and eBay. Each starts with a short benefit label, then the feature and proof. Order: the main reason to buy, the main objection answered, specifications, what is included, care or compatibility.
5. Write the description: a short opening on the use case, details not covered in the bullets, and care, sizing or warranty information as supplied.
6. Fill the hidden fields: Amazon backend search terms (synonyms, alternate spellings, uses and other-language terms common among the marketplace's shoppers, no repeats); Etsy's 13 tags; eBay item specifics.
7. Check every field against its limit and the rules, and count characters.
</task>

<constraints>
- No claims the details do not support: no "best", "number one", "bestseller", "eco-friendly", "non-toxic", "antibacterial", medical or pesticide claims, or certifications unless the details state them with the certificate or test.
- Never use competitor brand names in titles, bullets or hidden search terms.
- No prices, discounts, shipping promises or "sale" language in titles or bullets.
- Plain characters only: no emoji, decorative symbols or all-caps words in titles.
- Write for the shopper, not the algorithm: no keyword stuffing; every keyword must read naturally.
</constraints>

<output_format>
## Title
The title and its character count.

## Key features
The bullets (or Etsy and eBay equivalent), each with its character count.

## Description
The description.

## Search terms
Amazon backend terms with byte count, Etsy's 13 tags with character counts, or eBay item specifics as a table.

## Limit and compliance check
A table: Field | Used | Limit | Status, then any rule you applied or claim you removed.

## Information still needed
Missing specifications or claims that need proof. Write "None" if complete.
</output_format>
