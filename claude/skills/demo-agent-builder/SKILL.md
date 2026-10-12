---
name: demo-agent-builder
description: Builds or updates a Supademo Demo Agent using accessible knowledge, draft settings, indexing status, and readiness checks. Use for an agent setup or refresh; public publication and automation deliveries need to be included in the requested scope.
---

# Demo Agent Builder

Read [the tool conventions](../supademo-onboarding/references/tool-use.md).

1. **Resolve the agent.** Use `list_agents` and `get_agent` for an existing agent, or `create_agent` for an authorized new one. Establish its workspace, purpose, audience, and the knowledge the user wants it to use. If Agent tools are absent, explain the feature/review limitation.
2. **Configure the draft.** Use `update_agent` and `update_agent_intro` for requested identity, instructions, and introduction. Use `create_agent_quick_links` for new labels, `update_agent_quick_links` for existing labels, and `remove_agent_quick_links` for removals; read `get_agent` first and match labels case-insensitively. Use `list_agent_voices` if voice selection is needed. Read the schemas instead of copying demo voice/settings fields into Agent tools.
3. **Select knowledge.** Resolve source IDs with `search_agent_knowledge` or asset lists. Use `attach_agent_knowledge` for existing reusable sources, or the corresponding `add_agent_demo_knowledge`, `add_agent_video_knowledge`, `add_agent_document_knowledge`, and `add_agent_text_knowledge` tools for supported content. Uploaded document URLs must come from trusted workspace storage. Use `discover_agent_website_pages` and `add_agent_website_knowledge` only for the website/pages the user requested.
4. **Protect shared source metadata.** Providing demo/video `contentHints` can replace shared workspace hints used by other agents. A video source title only fills a source that has none. Omit these fields when only attachment is intended. Use `get_agent_knowledge_source` to review indexing state and attached content; read raw text only when necessary. `reindex_agent_knowledge` queues work and can re-crawl external websites.
5. **Check readiness.** Re-read `get_agent` and source status, use `evaluate_agent_checklist` when requested or appropriate for release readiness, and retrieve `get_agent_checklist`. Keep queued indexing/evaluation distinct from successful completion. Resolve failed/pending sources or report their status before claiming the agent is ready.
6. **Publish within scope.** `publish_agent` replaces the current live version; `unpublish_agent` removes live availability. Publish after the requested checks when publication is authorized, otherwise leave the draft and report what remains. Verify returned/live version state and, when possible, test the public agent with a relevant question.
7. **Configure automations separately when requested.** Inspect `list_agent_triggers` and connected integrations before using trigger tools. Enabled triggers can deliver conversation data by email or to external CRM/Slack/webhook integrations. Match recipients, actions, enabled state, and conditions to the user's request. Do not add or enable delivery as an incidental part of basic agent setup.

Use Monitor insight/session tools only for a requested investigation. Full transcripts and public session sharing are separate from aggregate agent readiness and can expose visitor information.
