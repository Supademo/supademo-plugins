---
name: deal-stage-demo-matcher
description: Recommends the right Supademo demo or showcase for a prospect based on deal stage, persona, and use case — with share links and send copy. Use when a rep asks "what should I send this account?"
---

# Deal Stage Demo Matcher

Stop sending the all-purpose overview demo to everyone. Match the asset to the moment.

## Prerequisites

- Supademo MCP connected
- Deal context: stage, persona, use case, and any objection on the table

## Workflow

1. **Intake.** Stage (first touch / evaluating / security review / negotiation), who's watching (champion, end users, exec sponsor, IT), and what they care about.
2. **Inventory the library.** `list_demos` and `list_showcases`, using `list_tags` to filter by use case. Note which assets exist per funnel stage.
3. **Match by stage logic:**
   - **First touch** → short outcome-led overview (≤10 steps); never the deep-dive
   - **Active evaluation** → feature deep-dives matched to their stated use case
   - **Multi-stakeholder** → a showcase bundling one asset per stakeholder, not five separate links
   - **Security/IT review** → admin, permissions, SSO demos
   - **Late stage / stalled** → the specific demo answering the open objection
4. **Return ranked picks.** Top 1–2 with a one-line "why this one," plus an existing verified share link. If personalized link creation is part of the request, use `create_demo_links` for demos or `create_showcase_links` for showcases. `get_showcase_share_info` supplies canonical showcase sharing information. A recommendation-only request does not require creating new links.
5. **Draft the send.** 2–3 sentence email/Slack copy referencing their context, with the link. Return the draft; sending requires a separate explicit request and an available authorized messaging tool.
6. **Flag gaps.** If no asset fits ("we have nothing for the CFO persona"), say so — that's roadmap input for the demo team.

## Guardrails

- Recommend from what exists; don't describe demos you haven't verified via `list_demos`.
- Prefer trackable links so `share-link-follow-up` can pick up the thread later.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
