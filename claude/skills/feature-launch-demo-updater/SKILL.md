---
name: feature-launch-demo-updater
description: Maps a product change or feature launch to the Supademo demos and steps it affects, then drafts the copy updates and flags steps that need recapture. Use when a release ships and demos show the old UI or outdated language.
---

# Feature Launch Demo Updater

Ship a feature without shipping stale demos. This skill finds every demo step a product change touches and drafts the fix.

## Prerequisites

- Supademo MCP connected
- A description of the change: release notes, a changelog entry, a PRD, or "we renamed X to Y and moved it to the settings page"

## Workflow

1. **Parse the change.** Extract what's user-visible: renamed features, moved navigation, new/removed buttons, redesigned screens, changed defaults.
2. **Find candidate demos.** Use `list_demos` (filter by relevant tags or folder via `list_folders` / `list_tags`) to shortlist demos likely to show the affected surface.
3. **Inspect each candidate.** Pull `get_demo` and scan step annotations, hotspot copy, and chapter titles for mentions of the old name, flow, or screen.
4. **Produce an impact report.**
   | Demo | Step(s) | What's stale | Fix type |
   Fix types: `copy-only` (text fix), `recapture` (screenshot shows old UI), `remove` (feature no longer exists).
5. **Apply authorized copy fixes** with `update_steps` and `update_hotspots`.
6. **Handle recaptures.** For steps flagged `recapture`, tell the user which screens to re-record. Once new media is uploaded (`create_upload_job` or via the media library with `list_media_library_items`), swap it in with `replace_step_media`.
7. **Tag for tracking.** Resolve or create the `needs-recapture` tag ID using `list_tags`/`create_tags`, then use `add_demo_tags` so unfinished work stays visible.

## Guardrails

- Keep edits and deletions within the user’s requested or approved scope; use exact step IDs.
- If a demo has translations (`list_demo_translations`), flag that they'll need regeneration after the source changes.
- Verify the updated content, then use `publish_demo` when the user has authorized publication; otherwise return the draft changes.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
