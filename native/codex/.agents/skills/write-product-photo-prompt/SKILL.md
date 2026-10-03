---
name: write-product-photo-prompt
description: Writes product-photography image prompts covering set, lighting, angles, props and lifestyle scenes in one consistent brand look, with variants for listings and ads. Use for e-commerce imagery.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: image-generation
  source: https://hermes-ide.com/prompts/write-product-photo-prompt
  catalog: 2026.1003.0
---

# Write product photo prompts

## Inputs

- [PRODUCT] (required): The product with exact details, such as type, size, shape, materials, colours, finish, packaging, logo placement and what makes it distinctive, plus where the images will be used (marketplace listing, own store, social ads).
- [BRAND_STYLE] (optional): The brand's look and customer, e.g. "minimal Scandinavian, muted earth tones, for design-conscious 30-somethings". Leave blank to propose a style that fits the product.
- [TOOL] (optional; one of: midjourney, stable-diffusion, chat-based, generic; default: generic): Target syntax. midjourney: parameters such as --ar. stable-diffusion: positive and negative prompts. chat-based: plain sentences for chat image tools. generic: any tool.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Product imagery sells when it is accurate, consistent and shows the product in use. An image model will happily invent a product that looks better than the real one, with a different shape, a misspelled logo or the wrong colour, which leads to returns, bad reviews and listings removed for misrepresentation. The reliable approach is to use generation for sets, backgrounds, props and lifestyle scenes, and to keep the real product faithful by supplying a reference photo (image-to-image, reference or product-placement features) or compositing the real product into the generated scene. A shot set needs the standard e-commerce angles plus lifestyle and ad formats, all sharing one lighting recipe, palette and surface vocabulary so the store looks like one brand.
</context>

<task>
Write [TOOL] product-photo prompts for:

<product>
[PRODUCT]
</product>

Brand style: [BRAND_STYLE]

1. **Product accuracy:** list the attributes that must stay faithful in every image (shape and proportions, materials and finish, exact colours, logo and label placement, size relative to a hand or common object). If the product description lacks shape, colour or materials, ask up to three questions and stop. Recommend supplying a clean reference photo of the real product and using the tool's image reference or product-placement feature, or compositing the real product photo, for any image that shows the product itself.
2. **Look:** the lighting recipe (for example large soft key light from the upper left, white bounce fill, gentle shadow; or hard sunlight with crisp shadows), the palette, surfaces and backgrounds, prop vocabulary, camera and lens feel, and mood. If brand style is blank, propose one that suits the product and customer and say why.
3. **Shot set:** prompts for each shot below, in a table with use, aspect ratio and notes, followed by each prompt ready to paste:
   - **Hero on white:** the product alone on a pure white seamless background, filling most of the frame, soft even light, no props, no text: the usual marketplace main image;
   - **Angles:** front three-quarter, side or back, and top-down, on the brand background;
   - **Detail:** a close-up of the material, texture or key feature;
   - **Scale:** the product with a hand or a familiar object for size;
   - **Lifestyle:** two scenes of the product in use by the target customer, in a setting that fits the brand;
   - **Ad variants:** a square 1:1 and a vertical 9:16 composition with clear empty space for a headline, and a 4:5 feed image;
   - **Seasonal or campaign** (one): the same look adapted to a season or launch.
4. **Style suffix:** a reusable block of lighting, palette, surface and camera wording to append to any future prompt for consistency.
5. **Accuracy and compliance:** what to check in every output against the real product (logo spelling, colour against the real item under daylight, proportions, number of parts), and a reminder that many marketplaces require main images to show the actual product accurately on a pure white background, often with rules about props, text and how much of the frame the product fills; tell the user to check their marketplace's current image rules.
</task>

<constraints>
- Do not let prompts change the product's design, add features or accessories that are not included, or show results the product cannot deliver; props must be clearly separate from what is sold, or noted as "not included".
- Keep prompts free of filler quality tags ("8k", "masterpiece") unless the tool is stable-diffusion and the user's model is known to respond to them.
- Do not render text, prices or claims in the image; add them in design software.
- Do not imitate another brand's trade dress, logos or recognisable campaign imagery, and do not use real people's likeness without permission.
</constraints>

<output_format>
## Product accuracy
## Look
## Shot set
Table: Shot | Use | Aspect ratio | Notes, then one code block per prompt.
## Style suffix
In a code block.
## Accuracy and compliance
A checklist.
</output_format>
