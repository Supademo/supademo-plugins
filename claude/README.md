# Supademo for Claude

Create, personalize, organize, and analyze interactive product demos from Claude. This plugin includes 25 workflow skills and a connection to Supademo's hosted MCP server. The skills guide Claude through tasks such as building a prospect showcase, improving demo copy, preparing voiceovers, reviewing translations, and explaining engagement results.

## Connect your account

1. Add the Supademo plugin from Claude's plugin directory, or upload the provided ZIP under **Customize → Plugins → Add → Upload plugin**.
2. Open the plugin's **Connectors** tab and add or connect **Supademo**. Sign in to your Supademo account and approve the connection through the sign-in flow.
3. On Team and Enterprise plans, your organization owner may need to add the connector first; each member then connects their own account.
4. Start a new conversation and describe what you want to accomplish. If you have several workspaces, name the one to use.

The plugin references `https://mcp.supademo.com/mcp`, the same endpoint as the Supademo connector. If that connector is already connected, use the existing connection. Installing skills does not sign you in or grant additional Supademo permissions. Never paste an access token into a conversation.

## Try a workflow

- “Find the onboarding demos in my Sales workspace and suggest which one to send to a finance buyer.”
- “Build a showcase for this prospect using these three demos, with an introduction and clear sections.”
- “Review this demo's copy for brand voice and give me a proposed revision.”
- “Summarize last month's demo performance and recommend one improvement.”

Describe whether you want a plan or saved edits. Include publication, deletion, or external delivery in the request when those actions are intended. The skills use the tools and permissions available to your connected account, and explain an unavailable action or measurement instead of inventing a result.

## Included skills

| Skill | Workflow |
| --- | --- |
| supademo-onboarding | Connect the intended account and resolve workspaces and assets. |
| brand-voice-editor | Align demo copy with brand voice and terminology. |
| chapter-pacing-organizer | Improve chapters, order, and pacing. |
| deal-stage-demo-matcher | Select demos for a prospect's stage and needs. |
| demo-agent-builder | Configure and check a Demo Agent using accessible knowledge. |
| demo-localizer | Manage translations and localization. |
| demo-personalizer | Apply prospect variables with fallbacks. |
| demo-qa-checklist | Review a demo before publication. |
| device-experience-auditor | Review device, browser, and country view shares. |
| exec-analytics-summary | Explain demo performance for a leadership audience. |
| feature-launch-demo-updater | Identify demo updates for a feature launch. |
| hotspot-dropoff-analyzer | Investigate engagement and hotspot activity. |
| persona-script-adapter | Adapt a demo's narrative for a buyer persona. |
| product-change-mapper | Map product changes to affected demos. |
| prospect-showcase-builder | Assemble a prospect's demo showcase. |
| share-link-follow-up | Draft follow-up using observed viewer engagement. |
| staleness-triage | Prioritize demos for refresh. |
| ticket-to-demo-script | Turn a ticket or product brief into a capture script. |
| top-performer-patterns | Extract patterns from successful demos. |
| trackable-link-generator | Create and organize sharing links. |
| translation-qa-reviewer | Review and correct translated copy. |
| video-to-demo-converter | Create a demo from uploaded video or prepared screenshots. |
| voiceover-producer | Prepare and generate demo voiceovers. |
| weekly-performance-digest | Prepare a periodic performance summary. |
| workspace-librarian | Organize the workspace library. |

## Availability and account access

Plugins are available on paid Claude plans. These skills work in Claude chat, Claude Desktop, and Cowork. Supademo workspace roles, subscription entitlements, and feature availability determine which tools the connected account can use. Some workflows require existing demo content, analytics, uploaded media, or enabled Demo Agents.

Selecting a workspace for a task does not restrict the connection to that workspace. The connection can reach workspaces accessible to your Supademo account. To revoke access, disconnect Supademo in Claude and revoke the corresponding connected-app/token authorization in Supademo.

## Data handling

The plugin supplies Markdown instructions and a remote connector reference. It includes no executable scripts, local MCP server, hooks, API keys, or separate plugin data store. Its workflow files do not send data to additional services on their own. Claude calls Supademo through the authenticated connector to read or change the assets needed for your request.

Requested Supademo actions can publish a demo or showcase, create sharing links, crawl supplied websites, generate media, or use connected integrations. Viewer/session investigations can return personal information, and enabled Agent automations can deliver information to configured recipients. Those actions remain subject to your request and Supademo's permissions. Supademo processes and retains service data according to its [Privacy Policy](https://supademo.com/privacy-policy).

## Support and license

- [Supademo help](https://supademo.com/help)
- [Supademo](https://supademo.com)
- [Terms of service](https://supademo.com/terms)

The plugin's distributable files are licensed under the MIT License in `LICENSE`. Access to the Supademo service is governed separately by its terms and account permissions.
