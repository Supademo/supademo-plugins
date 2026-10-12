---
name: demo-qa-checklist
description: Runs a structured pre-publish QA pass on a Supademo demo — typos, flow order, hotspot placement, dead links, chapters, voiceover and translation consistency. Use after editing a demo and before it goes live.
---

# Demo QA Checklist

Catch the embarrassing stuff before a prospect does. Runs a repeatable QA pass and returns a pass/fail checklist per demo.

## Prerequisites

- Supademo MCP connected
- The demo to check (name or ID; find it with `list_demos`)

## Workflow

Pull the full demo with `get_demo`, then walk every step in order and check:

1. **Copy quality** — typos, grammar, double spaces, inconsistent capitalization across steps, placeholder text ("Lorem", "TODO", "test").
2. **Flow coherence** — steps tell one continuous story; no orphan steps that jump context. Suggest `reorder_steps` if the sequence reads out of order.
3. **Hotspot sanity** — every step has a clear next action; hotspot copy under ~120 characters; no two hotspots with identical copy on the same screen.
4. **Links and CTAs** — inspect links and CTA targets in `get_demo`; `create_demo_links`, `update_demo_links`, and `delete_demo_links` mutate trackable links and is not an inspection tool. Check the returned targets: no empty hrefs, no localhost/staging URLs, UTMs present if the team uses them.
5. **Chapters** — long demos (15+ steps) have chapters; chapter titles match their content (`update_chapters` to fix).
6. **Voiceover consistency** — if some steps have voiceover and others don't, flag the gaps; mismatched voices across steps.
7. **Translation freshness** — use `list_demo_translations` with `targetLanguage` to inspect translated text. Compare it with the current source; do not invent a translation timestamp or claim staleness from metadata that is absent.
8. **Version note** — recommend `rename_demo_version` with a QA-passed label so the reviewed state is findable later.

## Output

A checklist per demo:

```
✅ Copy quality — clean
⚠️ Flow — step 7 references "the dashboard we just saw" but dashboard is step 9
❌ Links — step 12 CTA points to staging.acme.com
```

For a QA-only request, return findings. When fixes are requested or already approved, use `update_steps`, `update_hotspots`, `reorder_steps`, and `update_chapters` within that scope. Publication with `publish_demo` requires publication to be part of the user’s request. A metadata check alone does not prove hotspot placement, link reachability, or audio playback; mark those checks unverified until observed.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
