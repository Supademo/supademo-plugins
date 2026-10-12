---
name: weekly-performance-digest
description: Generates a recurring "top demos this week" digest from Supademo analytics — views, completion, CTA clicks, movers up and down — formatted for Slack or email. Use for a Monday-morning demo performance ritual.
---

# Weekly Performance Digest

The Monday-morning answer to "how are our demos doing?" — without opening a dashboard.

## Prerequisites

- Supademo MCP connected

## Workflow

1. **Pull the leaders.** `get_top_performing_demos` and `get_top_performing_showcases` for the last 7 days.
2. **Pull the trend.** Use equal UTC periods and the same explicit `viewType` and filters. Null deltas mean no prior baseline. Use response summaries for matching-population totals; the top-five page is not a workspace total.
3. **Enrich the top 5.** `get_demo_analytics` per top demo: views, unique viewers, completion rate, CTA click-through.
4. **Find the movers.** Demos that jumped or dropped meaningfully week-over-week — a demo that doubled its views because it got embedded somewhere new is the story, not the perennial #1.
5. **Format the digest:**

```
📊 Demo performance — week of {date}

Top demos
1. {name} — {views} views ({±}% WoW), {completion}% completion
...

📈 Mover of the week: {name} — {what changed}
📉 Worth a look: {name} — completion fell {x}pts
💡 One takeaway: {single actionable insight}
```

6. **Keep it short.** One screen of Slack. Numbers rounded. One insight, not five.

## Guardrails

- Never invent a "why" for a metric change — if the cause isn't visible in the data, say "worth investigating," not a fabricated explanation.
- Select the intended workspace from the request/context and `list_workspaces`; ask only if multiple matches remain ambiguous.
- A recurring digest needs a separate host scheduling capability and an explicit user request to schedule it. Formatting for Slack/email does not authorize sending; deliver a draft unless the user has explicitly requested delivery through an available messaging tool.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
