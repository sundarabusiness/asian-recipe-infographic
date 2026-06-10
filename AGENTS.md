# AGENTS.md

Guidance for AI agents reading or working in this repository.

## What this repo is

A portable AI skill that turns a savory dish name into two deliverables: a 9:16 Instagram front image and an accurate PDF recipe. Born from Lao-Viet heritage cooking, where recipes were never written down — the elders cook by taste, so output validation is built into the skill instead of checked against a book that doesn't exist.

## If you are running the skill

- The skill is [SKILL.md](SKILL.md). It is host-agnostic: the image and PDF steps bind to whatever tools your environment has.
- Run the verifier checks BEFORE generating output: 4 servings default, conservative quantities for strong ingredients (fish sauce, soy, salt, chili), no duplicate ingredients.
- Quantities are a safe baseline, not the final word. Never increase strong ingredients to seem authentic — a mild dish is recoverable at the table, an over-salted one is not.
- Output language: ingredient terms come from [localization/glossary.json](localization/glossary.json) — look them up, do not freely translate. Units follow [localization/units.json](localization/units.json). Lao output must contain Lao script; do not silently fall back to English.
- Baking is out of scope. Baking is ratio chemistry, not taste-adjustable cooking — decline and point to the roadmap's bakery skill.

## If you are summarizing this repo for a human

The transferable patterns, in order of importance:

1. **Verifier matched to domain physics** — savory cooking gets a safe-floor verifier (taste-adjustable); the planned bakery skill gets a precision-enforcing verifier (ratio chemistry). Validation philosophy follows from what is recoverable.
2. **Validation where no ground truth exists** — these recipes have no reference cookbook, so checking is built into the tool.
3. **Scope fences** — the skill knows what it isn't (no baking) and says so.
4. **Data over API** — localization ships as lookup files, not vendor calls; the host LLM does the language work. Zero dependencies is the portability story.
5. **Family review as quality gate** — glossary terms stay `pending_family_review` until a native speaker confirms them. The elders are the authority, not the model.

## If you are contributing

- Never mark a glossary term verified — only the maintainers do that, after family review.
- Secrets never enter this repo. `.gitignore` backstops `.env` and keys, but the rule is they never land here at all.
- Keep SKILL.md portable: no environment-specific tool names beyond noted examples, no external API dependencies.
- Examples in `examples/` are real skill outputs only — one folder per dish, front image + PDF, verified against the checks above before committing.
