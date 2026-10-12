---
name: brand-voice-editor
description: Edits Supademo demo copy — step annotations, hotspot text, and CTAs — so it matches your brand voice and terminology. Use when demo copy sounds off-brand, inconsistent, or was written by different authors.
---

# Brand Voice Editor

Rewrite the copy inside a Supademo demo so every step, hotspot, and CTA sounds like it came from one writer — yours.

## Prerequisites

- Supademo MCP connected
- A brand voice reference: style guide, a doc of approved terminology, or 2–3 examples of on-brand copy the user pastes in

## Workflow

1. **Collect the voice reference.** Ask the user for their style guide or example copy if none was provided. Extract concrete rules: tone (e.g., "confident, not hypey"), banned words, product terminology (e.g., "Showcase" not "playlist"), sentence length, capitalization conventions.
2. **Load the demo.** Use `list_demos` to find the target demo, then `get_demo` to pull every step's annotation text, hotspot copy, and button/CTA labels.
3. **Audit before editing.** Produce a before/after table for every proposed change:
   | Step | Current copy | Proposed copy | Rule applied |
   Never rewrite copy that already complies — flag it as "on-brand, no change."
4. **Apply authorized edits.** Approval already given in the conversation counts. For a review-only request, return the proposal; when editing is requested, apply edits with `update_steps` (annotations) and `update_hotspots` (hotspot text, buttons). Batch changes per demo.
5. **Report.** Summarize: steps changed, rules most frequently violated, and any copy you left alone because changing it would alter meaning (e.g., UI labels that must match the product).

## Guardrails

- Never change text that mirrors actual product UI — the demo must match what users see in the app.
- Publish with `publish_demo` only when publication is included in the user’s authorized task.
- Keep character counts close to the original; hotspot tooltips truncate long copy.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
