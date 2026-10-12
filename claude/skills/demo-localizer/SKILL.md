---
name: demo-localizer
description: Translates a Supademo demo into target languages, manages the translation lifecycle, and keeps a do-not-translate glossary. Use when expanding a demo library to new markets or when sales needs a localized version for a regional deal.
---

# Demo Localizer

One demo, every market. Generates and maintains translations without letting them drift out of sync with the source.

## Prerequisites

- Supademo MCP connected
- Target language(s) and, ideally, a glossary of terms that must not be translated (product names, feature names, trademarks)

## Workflow

1. **Check what exists.** `list_demo_translations` — regenerating an existing language overwrites manual fixes. Identify existing translations and regenerate only when that overwrite is part of the user’s authorized request.
2. **Build the glossary.** Ask for do-not-translate terms if none were given. Default protections: the product name, feature names that are UI labels, customer names in testimonials.
3. **Generate.** `generate_demo_translation` per target language.
4. **Spot-check the output.** Call `list_demo_translations` with `targetLanguage` for full translated entity text and media, then review the highest-stakes copy: step 1, all CTAs, and any step with numbers or claims. Verify:
   - Glossary terms survived untranslated
   - CTA labels stayed short enough for buttons
   - Formal/informal register matches the market (e.g., Sie vs du for German B2B)
5. **Fix in place.** Correct individual strings with `set_demo_translation_text` — don't regenerate the whole language for one bad line.
6. **Report.** Language, steps translated, fixes applied, and anything needing a native-speaker review.

## Lifecycle rules

- When source text changes, compare the corresponding translated entities against it. Flag affected strings for review; do not invent translation freshness timestamps. Regeneration overwrites manual fixes, so prefer targeted updates when appropriate.
- Remove abandoned languages with `delete_demo_translation` only on explicit request.
- Localized voiceovers are a separate pass — see the `voiceover-producer` skill with `list_voices` filtered to the target language.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
