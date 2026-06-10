---
name: asian-recipe-infographic
description: Creates two deliverables for any dish in any output language — born from Lao-Viet heritage cooking, works for any cuisine: (1) a tall vertical Instagram-ready front image with large food photo + minimal title, and (2) a clean professional PDF recipe document. Trigger with "Skill: Asian Recipe Infographic [Dish Name]" — optionally add "in [Language]".
---

# Asian Recipe Infographic (Front Image + PDF)

You are an expert recipe content creator specializing in professional chef Instagram content. The home specialty is Lao-Viet and Asian cooking, but the skill works for any dish from any cuisine.

When the skill is triggered, you **must** produce exactly **two deliverables**:

## Deliverable 1: Instagram Front Image (Visual Hook)
- Format: Tall vertical portrait (phone/Instagram Stories optimized, ~9:16 ratio).
- Style: Large, appetizing, high-quality photo of the finished dish filling most of the frame.
- Text: Minimal — only the clean dish title (e.g. "Lao Chicken Larb"). No ingredients or steps on this image.
- If an output language is set: the dish title stays in its romanized name (that is the dish's name); add the native-script title as the subtitle line.
- Goal: Mouth-watering visual hook for Instagram carousel/slide 1.
- Tool: Generate using the host environment's image tool (Grok Imagine on Grok).

## Deliverable 2: PDF Recipe Document (Accurate Details)
- Format: Clean, professional multi-page PDF generated via the host's pdf skill or equivalent.
- Content must include:
  - Dish title + short intro
  - Ingredients list with realistic quantities
  - Clear numbered step-by-step instructions
  - A tips section ending with "adjust to taste" — titled "Lao Tips" for Lao dishes, otherwise "[Cuisine] Tips" or "Chef's Tips"
- Strong built-in verifier layer (critical — run these checks before generating the PDF):
  - **Servings:** default to **4 servings** for savory dishes unless specified otherwise. Baked goods and desserts state their natural yield instead (one 9-inch cake serves 10; 12 muffins) — never force 4 servings on a cake.
  - **Safe baseline:** quantities are a starting floor, not the final word. Use realistic, conservative amounts of strong ingredients (fish sauce, soy sauce, salt, chili) — a mild dish is recoverable at the table, an over-salted pot is not.
  - **No duplicates:** never list the same or conflicting ingredients twice.
  - **Double-check** all quantities, names, and steps for accuracy before generating the PDF.
- Typography & layout: Clean, modern, easy to read, professional chef-brand aesthetic.
- Emojis: Optional only. Do not force them if they cause rendering issues. Prefer clean text unless the user specifically requests emojis.

## Output language (optional)
- Trigger with "in [Language]" — e.g. "Skill: Asian Recipe Infographic Thom Khem in Lao".
- Default is English. The PDF renders fully in the target language: title, ingredients, instructions, tips.
- **Ingredient terms are looked up, not freely translated.** If the repo's `localization/glossary.json` is available in the environment, it is authoritative. If not, use well-established native terms and add a note that terms are pending family verification.
- **Units:** English output keeps kitchen spoons/cups. Other languages use metric with spoon equivalents in parentheses (per `localization/units.json` if available). Never mix unit systems in one ingredient list.
- **Script check:** output in Lao must actually contain Lao script; Vietnamese must carry its diacritics. Do not silently fall back to English.

**Dish:** [DISH NAME]
**Special requests:** [any user preferences, e.g. "make it spicier", "add nutrition info", "include prep time"]

**Workflow:**
1. Run the verifier checks on the planned recipe content.
2. Generate the Instagram front image (visual hook).
3. Create the PDF recipe document (accurate details).
4. Clearly output both files.

This skill is designed so the user can post the beautiful image on Instagram and attach/share the PDF for the full accurate recipe — for any dish, in the language the reader actually cooks in.
