---
name: translation-qa-reviewer
description: Reviews machine-translated Supademo demos against a glossary and brand terminology, fixing errors string-by-string. Use before a localized demo ships to a regional campaign or gets embedded on a localized site.
---

# Translation QA Reviewer

Machine translation gets you 90% there. This skill finds the 10% that embarrasses you in front of native speakers.

## Prerequisites

- Supademo MCP connected
- A demo with at least one translation (`list_demo_translations`)
- Glossary / brand terminology list (ask if missing)

## Workflow

1. **Load both versions.** `get_demo` for the source, `list_demo_translations` with `targetLanguage` for full translated strings and entity IDs; without it, the tool returns language summaries.
2. **Run the checks, step by step:**
   - **Glossary violations** — product and feature names that got translated when they shouldn't be
   - **Truncation risk** — translated CTAs and hotspot copy significantly longer than source (German +30% is normal; flag anything that will overflow a button)
   - **Register** — consistent formal/informal address throughout; B2B defaults to formal in most markets
   - **Untranslated leftovers** — source-language strings that slipped through
   - **Broken variables** — numbers, dates, or placeholders mangled in translation
   - **False friends** — obviously wrong sense-for-sense choices (flag for native review rather than guessing)
3. **Fix what's certain.** `set_demo_translation_text` for glossary violations, leftovers, and truncations. Leave judgment calls flagged, not fixed.
4. **Output a QA report:**
   | Step | Issue | Severity | Fixed / Needs native review |

## Guardrails

- You are a safety net, not a substitute for one native-speaker pass before high-stakes launches. Say so in the report.
- Never regenerate the whole translation to fix individual strings — that destroys previous manual fixes.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
