---
name: share-link-follow-up
description: Uses identified Supademo viewer sessions and showcase details to draft a prospect follow-up grounded in observed engagement. Use before a check-in call; link-level session filtering and inferred buying intent are not available.
---

# Share Link Follow-up

Draft a useful follow-up from observed engagement while preserving the limits of identification and attribution.

## Workflow

1. **Define the account and assets.** Use the user's provided prospect context and known demo/showcase IDs. A personalized link does not prove the identity of everyone who opens or forwards it.
2. **Read supported data.** Use `get_demo_sessions` or `get_showcase_sessions`; use `get_showcase_session_details` when detailed showcase activity is needed. Session search supports email/name, not company or link ID. There is no link-ID session filter. Fetch all relevant pages for client-side company filtering using returned fields, and label any unresolved account attribution.
3. **Summarize evidence.** Report observed asset activity, completion, revisit counts, and last-view date where returned. Session rows represent viewer IDs, which may be multiple devices for one person. Completion alone does not establish the exact step where a viewer stopped, time spent on a specific section, forwarding, or buying-committee activity.
4. **Choose a useful next step.** Use supplied deal context and observed interests to suggest an explanation, shorter resource, or conversation. Separate hypotheses from observed facts. No recorded engagement means no recorded signal; it does not prove disinterest or email failure.
5. **Write the draft.** Keep it brief and at account level. Reference specific content only when the data supports that claim. Do not expose individual timestamps or private viewer details in outreach.
6. **Return the draft.** Sending requires an explicit user request and an available authorized messaging tool; this skill does not grant permission to contact anyone.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
