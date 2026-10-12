---
name: staleness-triage
description: Ranks the Supademo library by refresh priority using traffic, age, and performance — refresh now, refresh soon, archive. Use quarterly, or whenever "our demos are out of date" needs turning into an actual work queue.
---

# Staleness Triage

"We should update our demos" is a feeling. This skill turns it into a ranked queue.

## Prerequisites

- Supademo MCP connected

## Workflow

1. **Inventory.** `list_demos` for the full library. Read returned demo/version timestamps and state which timestamp represents the age signal; a version date is not necessarily the last source edit.
2. **Score each demo on two axes:**
   - **Exposure** — recent traffic from `get_demo_analytics`; is it embedded on high-traffic pages, in active showcases (resolve with `list_showcases`, inspect with `get_showcase`), in sales sequences? Mark embed/sequence placement unknown when that evidence is unavailable
   - **Staleness** — months since last edit, old branding/UI in captures, declining completion trend as a signal to inspect, not proof of outdated UI
3. **Triage into four buckets:**
   | Bucket | Rule | Action |
   | 🔴 Refresh now | High exposure × stale | Queue immediately |
   | 🟡 Refresh soon | Medium exposure × stale, or high exposure × slightly dated | Next cycle |
   | 🟢 Leave alone | Fresh, or stable performance | Nothing |
   | ⚫ Archive | No traffic in 90+ days, superseded | Move out of the active library |
4. **Make the queue durable.** Resolve or create `refresh-q3`/`archive-candidate` tag IDs with `list_tags`/`create_tags`, then use `add_demo_tags`; optionally move archive candidates to an Archive folder via `move_demos` when those exact moves are requested or approved. Moving is organization, not unpublishing; it may also affect public folder listings and connected integrations.
5. **Output** the triage table with per-demo evidence (traffic, last edit, trend) so priorities survive scrutiny.

## Guardrails

- Archive in this workflow means move/tag; do not infer permission to delete from an audit or archive request. Deletion needs a separate, explicit request identifying the assets.
- A low-traffic demo isn't automatically archivable — check whether it's load-bearing in a live showcase or embedded on a page before flagging it.
- Hand the 🔴 bucket to `feature-launch-demo-updater` or `demo-qa-checklist` to execute the actual refresh.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
