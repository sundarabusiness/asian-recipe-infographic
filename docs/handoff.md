# Handoff Document: Asian Recipe Infographic Skill

**Project:** Portable Chef Recipe Skill (Image + PDF)
**Owner:** Bobby Sundara (Chef Instagram Brand)
**Date:** June 2026
**Target:** Codex Pro Application / Cross-AI Portability (Grok → Claude)

---

## 1. Purpose of This Skill

This skill generates **two professional deliverables** for any Lao-Viet or Asian dish:

1. **Instagram Front Image** (Visual Hook)
   - Tall vertical portrait format (~9:16)
   - Large, appetizing food photo
   - Minimal clean title only
   - Designed as slide 1 for Instagram carousel

2. **PDF Recipe Document** (Accurate Details)
   - Clean, professional multi-page PDF
   - Accurate ingredients with realistic quantities (default 4 servings)
   - Clear numbered instructions
   - "Lao Tips" section with adjust-to-taste guidance
   - Strong built-in verifier layer to prevent bad measurements and duplicates

**Goal:** Allow a chef to post a beautiful visual on Instagram and share a clean, accurate PDF recipe.

---

## 2. Current State (as of June 2026)

**Origin location (Grok environment):**
`/home/workdir/.grok/skills/asian-recipe-infographic/SKILL.md`

**What Works Well:**
- Strong verifier layer (prevents duplicate ingredients, unrealistic measurements)
- Clean separation between visual hook (image) and accurate content (PDF)
- Professional chef-brand aesthetic
- Easy to trigger with natural language: `Skill: Asian Recipe Infographic [Dish Name]`

**Known Limitations:**
- Emojis in PDF can cause rendering issues in some environments (currently optional / disabled by default)
- Image generation sometimes produces minor text/layout drift (mitigated by strict prompts)
- PDF generation relies on the host environment having a working `pdf` skill or equivalent

---

## 3. Skill Structure (SKILL.md)

The skill follows the standard custom skill format: YAML frontmatter (`name`, `description`) plus a Markdown body. Key sections:

- Role framing (expert recipe content creator)
- Deliverable 1 spec: Instagram front image (tall vertical, large food photo, minimal title)
- Deliverable 2 spec: PDF recipe document (via the host `pdf` skill, verifier layer enforced)
- Workflow: image first, then PDF, output both files

See [../SKILL.md](../SKILL.md) for the full skill.

---

## 4. How to Use the Skill

**Trigger examples:**
- `Skill: Asian Recipe Infographic Chicken Larb`
- `Skill: Asian Recipe Infographic Thom Khem extra spicy`
- `Skill: Asian Recipe Infographic Banh Bao`

**Expected Output:**
- One tall vertical image file (Instagram front)
- One `.pdf` file (full recipe)

---

## 5. Verifier Layer (Important)

The skill contains a strong built-in verifier:

- Default to **4 servings**
- Realistic measurements only (never half-cups of fish sauce etc.)
- No duplicate or conflicting ingredients
- Double-check quantities before generating content

This was added after multiple rounds of image/PDF hallucination issues.

---

## 6. Portability Goals (for Codex Pro / Claude)

This skill is designed to be **portable** across AI environments.

**To port to Claude / other systems:**

1. Copy the `SKILL.md` content into the target environment's skills directory or system prompt.
2. Replace the image generation step with the host's image tool (or equivalent).
3. Replace the PDF generation step with the host's PDF/document tool (or use Markdown → PDF conversion).
4. Keep the verifier rules — they are the most important part for output quality.

**Recommended structure for other AIs:**
- Front: Generate tall vertical food photo + minimal title
- Back: Generate clean Markdown or PDF with ingredients + steps + tips
- Always run the verifier checks before final output

---

## 7. Codex Pro Application Goal

**Main Goal:** Get accepted into the Codex for Open Source program (six months of free access for open-source developers).

**Plan:**
- Host this skill (and future skills) in a public GitHub repo under my personal account.
- Use this skill as one of the portfolio pieces to show:
  - Real-world utility (chef content creation workflow)
  - Clean skill architecture + strong output validation (verifier layer)
  - Cross-AI portability design (made to work beyond just Grok)
  - Professional documentation (this handoff + SKILL.md)

---

## 8. Working Principles (for any AI continuing this project)

- Keep the **two-deliverable structure** (Instagram Front Image + PDF Recipe Document)
- Maintain and improve the **verifier layer** — it's one of the most important parts
- Make the skill as **portable** as possible so it can run on Claude, Grok, or other systems
- Keep documentation clean (update this handoff when big changes are made)
- Focus on quality and reliability over flashy features

---

## 9. Next Steps / Open Items

- [ ] Finalize PDF layout (current version is clean but can be improved)
- [ ] Add optional nutrition info section
- [ ] Test on 5–10 more dishes for consistency
- [x] Create GitHub repo structure for Codex Pro submission
- [ ] Decide on emoji policy (currently optional/disabled due to rendering issues)

---

## 10. Contact

**Bobby Sundara**
- X: [@bobbysundara](https://x.com/bobbysundara)
- Focus: AI tools for chef content + heritage preservation
- Current stack: Grok + Claude + local models
