---
name: top-performer-patterns
description: Reverse-engineers your best-converting Supademo demos into a reusable structural playbook — hook, length, chapter shape, CTA placement. Use before building new demos so they start from what already works.
---

# Top-Performer Pattern Extractor

Your best demos already know what converts. This skill writes it down.

## Prerequisites

- Supademo MCP connected
- Enough history for "top" to mean something (a handful of demos with real traffic)

## Workflow

1. **Identify the winners.** `get_top_performing_demos` supports server-side ranking by views, uniqueViews, or engagement. For completion or CTA engagement, fetch all relevant pages first, then sort the returned fields client-side, excluding null metrics and noting sample sizes. The returned population excludes showcases and unshared demos; do not call it the entire library.
2. **Dissect each.** `get_demo` per winner, plus `get_demo_hotspot_performance` for where viewers engage hardest. Record:
   - Total steps and estimated watch time
   - What step 1 shows — product outcome, problem statement, or UI tour?
   - Where the "aha" screen lands (step number)
   - Chapter structure and titles
   - CTA count and placement (mid-demo, end, both)
   - Voiceover: present or not; annotation length norms
3. **Find the pattern.** What do 4 of 5 share? Be honest when winners diverge — report "two archetypes" rather than forcing one template.
4. **Contrast with the laggards.** Pull 2–3 low-completion demos and note what the winners do that they don't. The differences are the playbook.
5. **Write the playbook:**

```
## Demo playbook — extracted {date}
- Length: {n}–{m} steps (~{x} min)
- Step 1: {pattern}
- Aha moment: by step {n}
- Chapters: {pattern}
- CTA: {pattern}
- Copy: {avg words}/step, {register}
Evidence: {demo} — {completion}%, {demo} — {completion}%...
```

## Guardrails

- Correlation caveat up front: top demos may win because of the feature they show, not their structure. The playbook is a strong prior, not a law.
- Re-run quarterly; patterns drift as the library and audience change.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
