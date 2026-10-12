---
name: trackable-link-generator
description: Creates trackable Supademo share links and a labeled registry per prospect, campaign, or channel — with naming conventions, UTM discipline, and expiry rules — while explaining attribution limits. Use when sharing demos anywhere you'll later want to know who watched.
---

# Trackable Link Generator

One generic share link tells you "someone watched." Separate links help organize distribution and personalization, but do not identify every viewer or provide a link-ID filter in session tools.

## Prerequisites

- Supademo MCP connected
- What's being shared (demo or showcase) and at what grain: per-prospect, per-campaign, or per-channel

## Workflow

1. **Pick the grain.**
   - **Per-prospect** — outbound and active deals; one link per account to organize personalization and distribution. `share-link-follow-up` can use identified-viewer data, but cannot filter sessions by that link ID
   - **Per-campaign** — launches, newsletters, paid; one link per campaign per asset
   - **Per-channel** — the same demo embedded on the site vs linked in email vs posted on social gets separate links, or attribution is guesswork
2. **Label the registry** so links stay legible at scale. The MCP link schemas do not have a link-name field; keep this human label in the registry:
   `{asset}--{campaign-or-account}--{channel}--{yyyymm}` (e.g., `onboarding-demo--acme-corp--outbound--202608`)
3. **Create the links.** `create_demo_links` for demos, `create_showcase_links` for showcases; use the URL and ID returned by link creation. `get_showcase_share_info` only provides canonical sharing/embed information. Pass a `links` array with `variables` and optional `expiresAt`; update operations change expiry/avatar colors, not variable values. Set expiry on deal-specific links where supported — a demo link in a lost deal's inbox shouldn't work forever.
4. **Add UTM discipline** for links landing in email/ads/social: consistent `utm_source` / `utm_medium` / `utm_campaign` matching the naming convention, so demo analytics and web analytics agree.
5. **Wire personalization (optional).** If the demo uses dynamic variables (see `demo-personalizer`), append the values as query params per link — `?v_name=Sam&v_company=Acme` (URL-encode each value; created link variables use keys without the `v_` prefix) — so each prospect's link renders their personalized demo.
6. **Output a link registry** the team can paste into the CRM or a sheet:
   | Link | Asset | Audience | Channel | Created | Expires |
7. **Close the loop.** Use `share-link-follow-up` for supported identified-viewer analysis. Session tools cannot filter by link ID. Analytics tools support `source`/UTM-source filtering, and `list_showcase_analytics_sources` lists showcase sources; source-level analytics are not proof of individual prospect identity.

## Guardrails

- Keep account-specific links separate so personalization and the distribution registry stay accurate; a distinct link alone does not prove account attribution.
- Keep personal data out of URL params beyond first name and company; emails, phone numbers, or anything sensitive belongs in a lead-capture form, not a query string.
- When requested, expire or delete the exact obsolete deal-room links with the supported link operation. There is no link-archive operation, and link expiry does not unpublish the canonical asset URL.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
