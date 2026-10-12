---
name: exec-analytics-summary
description: Converts raw Supademo analytics into a leadership-ready narrative — reach, engagement, CTA activity, and one recommendation. Use for QBRs, board updates, or justifying the demo program's budget.
---

# Exec Analytics Summary

Executives don't want completion rates; they want to know if the demo program is working. This skill translates.

## Prerequisites

- Supademo MCP connected
- The reporting period (quarter, month) and the audience (CMO, board, sales leadership)

## Workflow

1. **Aggregate the period.** List accessible demos with `list_demos(scope: "workspace")` and showcases with `list_showcases(scope: "workspace")`, following every page of both lists. Call `get_demo_analytics` for each demo, passing its returned `id` as `demoId`, and `get_showcase_analytics` for each showcase, passing its returned `id` as `showcaseId`. Use the same workspace, reporting dates, and applicable filters. These analytics tools require individual asset IDs; they do not accept a workspace-only query. Use `get_top_performing_demos` / `get_top_performing_showcases` for standouts and matching-population totals. Report any inaccessible assets or failed calls as coverage gaps.
2. **Compare like periods.** Specify UTC dates and the same `viewType`/filters for each call. Use top-performing responses’ `summary.totalViews` for their matching population, not a sum of the returned top-N page. Keep demos and showcases separate to avoid counting a showcase visit and its nested demo view as one deduplicated audience. A null previous-period delta means no prior baseline, not +100% growth.
3. **Structure the narrative — five beats, one page:**
   - **Reach** — views and per-asset unique viewers, labeled with their actual definitions; do not add per-asset unique viewers into a workspace-wide people count
   - **Engagement** — did they actually watch (completion), and where do they lean in (`get_demo_hotspot_performance` on the top demo)
   - **Conversion** — CTA click-throughs; demos that hand off to trials/sales calls
   - **Standouts** — the one demo or showcase that outperformed, and the honest laggard
   - **Recommendation** — one concrete next move (double down, refresh, kill)
4. **Write for the audience.** No tool jargon ("hotspot," "step") — translate to "the pricing section," "the setup walkthrough." Percentages over raw counts unless raw counts impress.

## Output

A one-page summary in markdown, ready to paste into a doc or deck, with an appendix table of per-demo numbers for the detail-oriented.

## Guardrails

- Views and CTA clicks do not establish a trial, booked meeting, influenced revenue, or pipeline result. Include those claims only with separately provided and attributable business data; never imply causation from engagement alone.
- Flag data gaps honestly (e.g., demos with no UTM discipline can't be traced to campaigns).

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
