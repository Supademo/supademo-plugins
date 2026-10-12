---
name: product-change-mapper
description: Cross-references a changelog or upcoming release against the Supademo library and flags every demo a product change will touch — before it ships. Use in release planning so demo updates land with the launch, not weeks after.
---

# Product Change Mapper

The release notes say "redesigned settings page." This skill answers the question nobody asked in the launch meeting: which 9 demos show the old settings page?

## Prerequisites

- Supademo MCP connected
- The change list: changelog, release notes, or a launch plan (works for shipped *and* upcoming changes)

## Workflow

1. **Decompose the changes.** For each item, note the affected surface (screen/flow), the change type (rename, redesign, move, remove, add), and whether it's shipped or upcoming.
2. **Sweep the library.** `list_demos` with `list_folders`/`list_tags` to narrow by product area, then `get_demo` on candidates. Match on step copy mentioning the feature, chapter titles, and captures of the affected screens.
3. **Build the impact matrix:**
   | Change | Demo | Steps affected | Severity | When |
   Severity: **breaking** (demo now shows wrong/missing UI), **cosmetic** (looks dated, still accurate), **copy-only** (terminology drift).
4. **Sequence the work.** Breaking changes on high-traffic demos first (cross-reference `get_demo_analytics`). For upcoming changes, note the ship date so recaptures are scheduled for launch day, not discovered after.
5. **Mark and hand off.** For authorized tagging, resolve or create the `impacted-{release}` tag ID using `list_tags`/`create_tags`, then apply `add_demo_tags` and pass the queue to `feature-launch-demo-updater` for execution.

## Guardrails

- For a mapping-only request, return the report without changing content; apply tracking tags only when requested. Keeping mapping separate from fixing means the impact report can go in the launch plan as-is.
- For upcoming changes, never edit demos early — the live demo must match the live product until ship day. Suggest `duplicate_demo` to prep the updated version in parallel, swapping at launch.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
