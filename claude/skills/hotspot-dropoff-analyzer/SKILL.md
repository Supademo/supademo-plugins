---
name: hotspot-dropoff-analyzer
description: Analyzes Supademo completion, step engagement, and hotspot click counts to identify likely friction. Use when a demo gets traffic but completion is low; report hypotheses without presenting these metrics as an exact abandonment funnel.
---

# Hotspot Drop-off Analyzer

Find likely friction in a demo and tie each recommendation to available evidence.

## Workflow

1. **Collect comparable data.** Use the same UTC dates and `viewType` for `get_demo_analytics`, `get_demo_hotspot_performance`, and any needed `get_demo_sessions`. Fetch all relevant pages before filtering sessions.
2. **Keep metric meanings intact.** Hotspot performance contains click events, which can include repeated clicks. Step `viewersReached` is an engagement-weighted measure and need not form a monotonic funnel. Session completion is a percentage of steps reached, not a reliable chronological exit step. Do not derive an exact abandonment count, last step, or unique-viewer conversion rate from these fields.
3. **Identify signals.** Report the demo's completion measure, steps with relatively low engagement, and CTA or hotspot click patterns. Check final CTA activity before treating low end-step engagement as failure. Note small samples and unavailable values.
4. **Inspect the content.** Pull `get_demo` for candidate steps. Look for unclear next actions, competing hotspots, long copy, unexplained screen changes, early forms, and repetitive setup. Treat explanations as hypotheses until actual playback or additional evidence supports them.
5. **Review audience context.** `get_device_analytics` can show OS/browser view shares. It cannot show that mobile visitors abandon faster; use an actual mobile playback check for layout evidence.
6. **Recommend changes.** Return Step | Evidence | Hypothesis | Proposed fix | Tool. Use `update_steps`, `update_hotspots`, `reorder_steps`, `delete_steps`, or `update_chapters` for authorized fixes, then compare the same metrics over a later comparable period.

State what remains unmeasured. A content change and a later metric increase do not by themselves establish causation.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
