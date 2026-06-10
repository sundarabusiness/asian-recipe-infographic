# Multilingual output layer — v1 spec

Any dish, any language. The recipe skill gains an output-language parameter so the same dish renders for the grandmother and the grandkid in one run.

## How it works

No translation API. The skill runs inside an AI host (Grok, Claude, Codex), and the host model does the language work — guided by two data files that handle the parts where machine translation fails quietly:

- [glossary.json](../localization/glossary.json) — ingredient terms are **looked up, not translated**. "Fish sauce" must come out as ນ້ຳປາ in Lao and nước mắm in Vietnamese every time, not whatever the model improvises that day.
- [units.json](../localization/units.json) — measurement conventions per language. English keeps kitchen spoons; Lao and Vietnamese output goes metric with spoon equivalents in parentheses.

This keeps the skill at zero dependencies, which is the point of the whole project.

## Triggering

```
Skill: Asian Recipe Infographic Tam Mak Houng in Lao
Skill: Asian Recipe Infographic Thom Khem in Vietnamese
```

Default output language is English. v1 supported set: English, Lao, Vietnamese.

## What changes per language

- **PDF recipe**: fully in the target language — title, ingredients (glossary terms), instructions, Lao Tips section.
- **Front image**: dish title stays in its romanized form (that is the dish's name), with the native-script title added as the subtitle line.

## Verifier additions

The existing verifier rules (4 servings, realistic quantities, no duplicates) apply unchanged. Localized output adds:

1. **Script check** — Lao output must actually contain Lao script characters; same for Vietnamese diacritics. Catches the failure where the model silently answers in English.
2. **Glossary compliance** — every ingredient that has a glossary entry must use it.
3. **Unit consistency** — one unit system per ingredient list, per units.json conventions.

## The family review rule

Every glossary term ships as `pending_family_review` and is only marked verified after a native speaker in the family confirms it. There is no cookbook to check against — the elders are the reference. This is the project's quality model: the model drafts, the family verifies.

## Known hard problem (scheduled last)

Lao script in generated PDFs. Complex script shaping and font embedding break most PDF generators — the same class of problem as the emoji rendering issue documented in the handoff. This gets its own issue and its own commits once the spec, glossary, and verifier checks are stable.

## Out of scope for v1

- Input in languages other than English (roadmap)
- Languages beyond the v1 set (roadmap — the glossary structure already supports adding columns)
