---
name: prospect-showcase-builder
description: Assembles a personalized Supademo showcase for a specific account — curated demos, ordered sections, personalized intro, trackable link. Use for high-value deals that deserve more than a pasted demo link.
---

# Prospect Showcase Builder

A digital sales room in five minutes: the three demos this account actually needs, in the order they should watch them.

## Prerequisites

- Supademo MCP connected
- Account context: company, evaluating team, use case, stakeholders, stage

## Workflow

1. **Curate ruthlessly.** From `list_demos` (filtered by tags), pick 3–5 demos — not ten. Order tells the story:
   1. The outcome overview (why care)
   2. Their use case deep-dive (why us)
   3. Stakeholder-specific proof (security for IT, reporting for the exec)
2. **Propose before building.** For a planning request, show the picks, order, and section grouping. For an authorized build request, proceed with a reasonable selection and state the assumption.
3. **Build.** `create_showcase` creates a published showcase by default. If a private draft is needed, immediately set `sharing.visibility: "private"` with `update_showcase_settings`; do not imply the creation itself was atomic/private. Then `create_showcase_sections` for new grouping (e.g., "Start here" / "For your team" / "For IT") and `add_showcase_content` to slot demos.
4. **Personalize the wrapper.** Intro copy naming the account and their goal — one warm sentence, not a pitch. Add approved external resources via `add_showcase_content` with `contentType: "link"` and a `url`; use `update_showcase_settings` for the showcase CTA. `create_showcase_links` creates personalized/trackable sharing links, not outgoing resource links.
5. **Get the trackable link.** Create an account-specific link through `create_showcase_links` with a `links` array containing permitted variables/expiry; use the returned ID and URL. `get_showcase_share_info` returns canonical sharing/embed information and does not create a personalized link. Session tools have no link-ID filter and do not identify every anonymous or forwarded viewer.
6. **Hand to the rep** with the link and suggested send copy.

## Reuse pattern

For repeated deal shapes, build once and `duplicate_showcase` per account, personalizing only the intro — 90 seconds per deal after the first.

## Guardrails

- Create within the user’s requested scope. Reuse an existing approved template where suitable, and verify the returned showcase and section IDs.
- Resolve or create workspace tag IDs with `list_tags`/`create_tags`, then tag account-specific showcases using `add_showcase_tags` for the account and `deal-room` so they're findable and archivable when the deal closes.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
