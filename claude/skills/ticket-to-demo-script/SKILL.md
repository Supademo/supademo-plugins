---
name: ticket-to-demo-script
description: Converts an engineering ticket, PRD, or changelog entry into a first-draft Supademo demo script — the click path to capture, per-step copy, and chapter breaks. Use when a feature ships and marketing needs its demo yesterday.
---

# Ticket to Demo Script

From "PROJ-142: Implement bulk CSV export" to a capture-ready demo script in one pass.

## Prerequisites

- Supademo MCP connected (for the build step; scripting works standalone)
- The ticket/PRD text — pasted, or pulled via a connected issue tracker

## Workflow

1. **Extract the user-facing story.** From the ticket, answer: Who asked for this? What could they not do before? What's the happy path? Ignore implementation details — the demo shows outcomes, not architecture.
2. **Draft the capture plan.** The exact click path to record, screen by screen:
   ```
   1. Dashboard → the entry point (establishes context)
   2. Click {feature entry} → the moment of discovery
   3–5. The core flow, one decision per step
   6. The result screen → proof it worked
   7. CTA
   ```
   Flag any screen needing seeded data ("account must have 3+ projects for this to look real").
3. **Write per-step copy.** Annotation (≤25 words, labels the action) and optional voiceover line (spoken register) for each step. Lead step 1 with the outcome, not the feature name.
4. **Suggest structure.** Chapter breaks if 10+ steps; where the CTA lands; tags to apply.
5. **Hand off for capture.** A human records the flow in Supademo.
6. **Build after capture.** Once steps exist, apply the script with `update_steps`. Create new chapter steps with `create_steps` using `type: "chapter"`, `chapterType: "Link"`, the title in `chapter.heading`, and the planned 1-based `position`; use `update_chapters` only to edit existing chapter step IDs. Apply hotspot CTAs with `update_hotspots` and optionally `generate_voiceovers`.

## Guardrails

- If the ticket is ambiguous about user-facing behavior, list the assumptions at the top of the script rather than guessing silently.
- Check `list_demos` first — the feature may already have a demo to update instead (see `feature-launch-demo-updater`).

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
