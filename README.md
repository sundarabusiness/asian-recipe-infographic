# Asian Recipe Infographic

An AI skill that turns any Lao-Viet or Asian dish name into two ready-to-post deliverables:

1. **Instagram front image** — a tall vertical (9:16) visual hook: large appetizing food photo, minimal clean title, built as slide 1 of a carousel.
2. **PDF recipe document** — a clean, professional multi-page recipe: realistic ingredient quantities (4 servings by default), numbered steps, and a "Lao Tips" adjust-to-taste section.

Built for a working chef's Instagram workflow: post the beautiful image, share the accurate PDF.

## Why this exists

There is no cookbook for these dishes. The recipes live with the elders, who cook by taste — ask how much fish sauce goes in and the answer is "I don't know, you taste it." That works standing in a kitchen next to your grandmother. It does not survive distance or generations.

This skill writes the recipes down: quantified for someone learning alone (4 servings, realistic measurements), with the traditional method kept where it belongs — a "Lao Tips" section that ends every recipe the way the elders would: adjust to taste.

It also explains the verifier layer. A normal recipe can be checked against a book. These can't, because the book doesn't exist. When there is no reference to fact-check against, the validation has to be built into the tool itself.

One more thing the quantities are not: the final word. Every palate is different — some want it spicier, some want double the padek. The numbers here are a safe baseline, because salt you can add at the table but you cannot take back out of the pot. The recipe keeps you from ruining the dish; the tips tell you where to push it. That is also why the verifier rejects large amounts of strong ingredients — a mild baseline is recoverable, an over-salted pot is not.

## Quick start

Drop [SKILL.md](SKILL.md) into your AI environment's skills directory, then trigger with natural language:

```
Skill: Asian Recipe Infographic Chicken Larb
Skill: Asian Recipe Infographic Thom Khem extra spicy
Skill: Asian Recipe Infographic Banh Bao
```

You get back one tall vertical image and one `.pdf` recipe file.

## The verifier layer

The most important part of this skill is not the prompt — it's the built-in output validation. Recipe generation is a classic LLM hallucination zone (half-cups of fish sauce, duplicate ingredients, quantities that drift between the image and the document). After multiple rounds of bad outputs, the skill now enforces:

- **4 servings by default** — every quantity anchored to a known serving count
- **Realistic measurements only** — sanity bounds on strong ingredients (fish sauce, soy sauce, chili)
- **No duplicate or conflicting ingredients** — one canonical ingredient list
- **Double-check before generation** — quantities, names, and steps verified before the PDF is rendered

If you adapt this skill, keep the verifier rules. They are the difference between a demo and a tool a chef actually uses.

## Portability

The skill is written to run across AI environments, not locked to one vendor:

| Environment | Image step | PDF step | Status |
|---|---|---|---|
| Grok | Grok Imagine | `pdf` skill | Working (origin environment) |
| Claude | Image tool or prompt handoff | PDF/document skill or Markdown→PDF | Ported by design — see [docs/handoff.md](docs/handoff.md) |
| Other | Any text-to-image API | Any Markdown→PDF path | Adapt the two tool bindings, keep everything else |

The skill body is plain Markdown with YAML frontmatter — the only environment-specific parts are the two tool bindings (image generation and PDF rendering). Porting means swapping those two lines.

## Repo contents

| Path | What it is |
|---|---|
| [SKILL.md](SKILL.md) | The skill — drop-in ready |
| [docs/handoff.md](docs/handoff.md) | Full project handoff: design decisions, verifier rationale, porting guide |
| [examples/](examples/) | Sample outputs (front images + recipe PDFs) |

## Roadmap

- [ ] **Multilingual output — in progress.** Any dish, any language: same recipe renders for the grandmother in Lao and the grandkid in English. Spec and glossary at [docs/localization-spec.md](docs/localization-spec.md); v1 set is English, Lao, Vietnamese
- [ ] Sample outputs for 5–10 dishes in `examples/`
- [ ] **Bakery skill** (separate skill, planned) — baking is ratio chemistry, not taste-adjustable: bake by taste and you get rocks. It needs the opposite verifier philosophy: instead of protecting a safe baseline, the verifier enforces precise measurements, ratios, and temperatures. Same two-deliverable architecture, inverse validation — which is the point of building verifiers per domain
- [ ] Direct image-API integration (scripted generation instead of in-environment tool call)
- [ ] Optional nutrition info section
- [ ] Finalized PDF layout pass
- [ ] Emoji policy decision (currently disabled by default — rendering issues in some PDF environments)

## Author

**Bobby Sundara** — AI tools for chef content + Lao-Viet heritage preservation.
X: [@bobbysundara](https://x.com/bobbysundara)

## License

[MIT](LICENSE)
