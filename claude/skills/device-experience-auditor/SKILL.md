---
name: device-experience-auditor
description: Reviews Supademo OS, browser, and country view shares and identifies demos worth checking on mobile. Use for a mobile campaign or accessibility review; device-specific completion rates are unavailable from these tools.
---

# Device Experience Auditor

Use audience data to prioritize a mobile playback review without inventing device conversion metrics.

## Workflow

1. **Set the scope.** Select the workspace and UTC period. Pass `viewType` explicitly. `get_device_analytics` without `demoId` combines demo and showcase traffic; pass a demo ID for a demo-specific view.
2. **Read the returned breakdowns.** Report OS and browser view shares and their `truncation` flags. These are top-five lists, so missing entries can be in the long tail. Country shares exclude unknown locations and need a coverage caveat.
3. **State the measurement limit.** The tool does not return device classes, per-device completion, or a mobile-versus-desktop conversion gap. OS names can suggest mobile traffic, but label that interpretation and avoid an exact mobile total when the list is truncated or ambiguous.
4. **Inspect candidates.** Use `get_demo` to review screenshot density, annotation length, and hotspot layout. If browser access is available, check actual playback at a mobile viewport and a desktop viewport. Distinguish observed layout problems from hypotheses based on metadata.
5. **Recommend priorities.** Rank by measured traffic and observed usability problems. Suggest a shorter duplicate, clearer annotations, or recapture at a useful zoom. Do not calculate a traffic-times-completion-gap score when completion by device is unavailable.
6. **Report.** For each demo, include the period, audience scope, observed OS/browser shares, truncation, playback evidence, and recommended action. Keep audit-only requests read-only; carry out fixes when the user has requested them.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
