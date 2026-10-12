---
name: chapter-pacing-organizer
description: Restructures long Supademo demos with chapters and tighter pacing so viewers can jump to what they care about. Use when a demo has grown past ~15 steps, has no chapters, or analytics show mid-demo drop-off.
---

# Chapter & Pacing Organizer

Long demos lose viewers. This skill breaks a demo into skimmable chapters and trims the fat.

## Prerequisites

- Supademo MCP connected
- The demo to restructure

## Workflow

1. **Read the demo end-to-end.** `get_demo` — map each step to the task it belongs to (e.g., steps 1–4 = "Connect your account", 5–9 = "Build your first report").
2. **Propose chapter breaks.** Chapters should follow task boundaries, not arbitrary step counts. 3–6 chapters is the sweet spot. Present:
   | Chapter | Steps | Title |
3. **Spot pacing problems.**
   - Consecutive steps showing near-identical screens → candidates to cut or consolidate through an explicitly planned edit; no generic step-merge tool is available
   - Setup steps a buyer doesn't care about → cut or collapse into one annotated step
   - The "aha" moment buried past step 10 → suggest moving it earlier with `reorder_steps` if the flow allows
4. **Apply the authorized plan.** Create missing chapter steps with `create_steps`: use `type: "chapter"`, `chapterType: "Link"`, the title in `chapter.heading`, and `position` for the intended 1-based insertion point. Edit existing chapters with `update_chapters` using their chapter step IDs. Use `reorder_steps` for sequence changes and `delete_steps` for the exact deletions the user has authorized. Existing authorization counts; ask only when the targets or scope remain unclear.
5. **Verify.** Re-pull `get_demo` and confirm the chapter list and step order match the approved plan.

## Guardrails

- Identify exact step IDs before deletion and keep the change within the requested scope.
- If the demo has voiceovers, warn that reordering may break narrative continuity — voiceover scripts may need regeneration (`generate_voiceovers`).
- Check `get_demo_hotspot_performance` first if available: don't cut steps that are actually engaging viewers.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
