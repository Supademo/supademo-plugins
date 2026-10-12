---
name: workspace-librarian
description: Audits and tidies the Supademo workspace — naming conventions, tags, folder structure, duplicates, and orphaned drafts. Use when nobody can find anything, or quarterly before it gets that way.
---

# Workspace Librarian

Every demo workspace drifts toward "Untitled (3)" and a folder called "misc." This skill drifts it back.

## Prerequisites

- Supademo MCP connected

## Workflow

1. **Take inventory.** `list_folders`, `list_demos(scope: "workspace")`, `list_showcases(scope: "workspace")`, `list_tags` — the map of accessible workspace assets and where they belong. Follow all pages of both asset lists, including teammates' shared content. Traverse child folders with `list_folders`, passing each listed folder's `id` as `parentId`; another user's private assets remain outside this inventory.
2. **Audit against library hygiene rules:**
   - **Naming** — inconsistent patterns ("Onboarding Flow" vs "demo_onboarding_v2_FINAL"); propose one convention: `{Product area} — {Flow} ({Persona/variant})`
   - **Tags** — untagged demos, near-duplicate tags (`sales` vs `Sales` vs `sales-team`), tags used once
   - **Folders** — empty folders, junk-drawer folders, demos sitting at root
   - **Duplicates** — same flow captured twice; use `get_demo_analytics` to recommend which to keep and propose organizing the other with folders/tags. Removing a duplicate requires explicit authorization identifying the asset. `merge_demos` combines content into a new demo and preserves every source; it does not remove duplicates.
   - **Orphaned drafts** — unpublished demos untouched for 60+ days
   - **Expired deal rooms** — account-specific showcases (`deal-room` tag) for closed deals
3. **Propose the cleanup plan** — a full change list grouped by action, with counts. Nothing executes yet.
4. **Apply the authorized plan, in dependency order.** Existing user authorization counts; for a review-only request, stop at the change list:
   - Renames via demo/folder updates and `rename_folder`
   - Tag consolidation via `create_tags`, `update_tags`, and `delete_tags`. Resolve tag IDs first; use `add_demo_tags`/`add_showcase_tags` to preserve unrelated associations and `remove_demo_tags`/`remove_showcase_tags` to detach only superseded tags. Workspace tag deletion detaches the tag from every demo/showcase, so include all affected assets in that change’s scope
   - Moves via `move_demos` / `move_showcases`
   - Content combinations via `merge_demos` only when the user requests a combined demo from the exact source IDs in the authorized plan; verify the returned new demo ID and content. Keep this separate from duplicate cleanup, and preserve the originals unless their removal is explicitly authorized
   - Empty folders last via `delete_folder`. Immediately before deletion, re-read the folder's entry through `list_folders` for its parent and confirm `demoCount`, `showcaseCount`, `videoCount`, and `childFolderCount` are all zero. A missing entry, permission failure, or incomplete inventory does not establish emptiness. Skip any folder whose emptiness cannot be verified; deleting a non-empty folder can archive demos, move showcases, or delete library videos
5. **Report** before/after counts: untagged 34 → 0, root-level demos 12 → 0, tags 61 → 28.

## Guardrails

- Do not infer permission to delete demos or showcases from a cleanup request. Archive here means organizing with folders/tags, and does not unpublish an asset. Deletion needs an explicit request identifying the assets.
- Verify merge source IDs, the returned new demo ID, and resulting content before moving on. Do not count a merge or folder/tag move as removing duplicates. Ask only for missing scope or authorization; do not repeat approvals the user has already supplied.
- Save the naming convention to the team's docs so the drift restarts slower.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
