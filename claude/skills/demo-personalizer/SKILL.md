---
name: demo-personalizer
description: Injects dynamic variables ({{name}}, {{company}}) into the right places in a Supademo demo — title, step copy, hotspots, chapters, CTAs — with graceful fallbacks, then wires per-prospect URLs. Use to turn one demo into a 1:1 asset for every account.
---

# Demo Personalizer

"See how Acme cuts onboarding time in half" converts better than "See how our customers cut onboarding time in half." This skill finds the places where that's true — and only those.

## Prerequisites

- Supademo MCP connected
- The demo to personalize, and which variables the team can actually supply (`name`, `company`, `role`, …) via URL params or lead-capture form fields

## Workflow

1. **Sweep the demo.** `get_demo` — collect the title, every step annotation, hotspot copy, chapter titles, and CTA labels.
2. **Pick insertion points that earn it.** Personalization works at moments of attention, not everywhere:
   - **Demo title** — "How {{company}} automates onboarding" (via `update_demo_settings`)
   - **Step 1 hook** — the first line they read; naming them here sets the frame
   - **The CTA** — "Start {{company}}'s free trial" outperforms generic
   - **One mid-demo re-engagement** — a chapter title or annotation right where analytics show attention sagging
   Cap it at **3–5 insertions**. A demo that says the prospect's name on every screen reads as mail-merge, not attention.
3. **Write fallbacks for every variable.** Organic and ungated viewers arrive with no values — "How {{company|your team}} automates onboarding" must render as "How your team automates onboarding," never as raw `{{company}}`. No insertion ships without a fallback.
4. **Prepare the plan** — Location | Current copy | Personalized copy | Fallback render. Return it for a planning request; carry out edits already authorized by the user without repeating approval.
5. **Apply.** `update_steps` for annotations, `update_hotspots` for hotspot copy, `update_chapters` for chapter titles and chapter-button CTA labels, `update_demo_settings` for the title.
6. **Wire the data source.**
   - **Outbound / 1:1** — query params on per-prospect links from `trackable-link-generator` (`?v_company=Acme`); at scale, the email tool's merge fields fill the URL (`?v_company={{account.name}}`; URL-encode rendered values)
   - **Inbound / gated** — map lead-capture form fields to the same variables
7. **Test both states.** Use the returned canonical or trackable URL. Created link variables use unprefixed keys such as `company`; URL overrides use the `v_` prefix. View once with values populated and once bare, confirming the personalized and fallback renders both read cleanly.

## Guardrails

- Personalize framing, never facts — "{{company}}'s dashboard" is a lie if the screens show your own sample data. Frame around the viewer; don't fake their environment.
- First name and company only in URL params; anything more personal goes through the lead form.
- If the demo has translations, personalization spans need the same treatment per language (`set_demo_translation_text`) or locked-out variables will leak English into localized demos.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
