---
name: supademo-onboarding
description: Connects a Supademo workflow to the intended account and workspace, resolves accessible assets, and explains missing tools or permissions. Use at first connection or when a demo, workspace, or feature cannot be found.
---

# Supademo Onboarding

Read [the tool conventions](references/tool-use.md) before using Supademo tools.

1. If the MCP connection requires authentication, use the host's Supademo sign-in flow. Do not ask the user to paste an access token into chat.
2. Call `list_workspaces`. Use a workspace named in the request or already selected in context. Ask a short clarifying question only when multiple accessible workspaces still match.
3. Resolve asset IDs with `list_demos`, `list_showcases`, `list_agents`, or `list_media_library_items`. Use returned names, IDs, pagination, and visibility; do not infer that an empty first page means the asset is absent.
4. Use `get_workspace_settings` when workspace configuration matters. Role, plan, and feature flags govern what the connection can do. Missing Agent or video tools can reflect a feature gate or a pending platform review; do not invent or call undiscovered tools.
5. Continue the requested workflow with the resolved workspace and asset IDs. If a permission or entitlement blocks it, explain the concrete limitation and any useful work that can still be completed. The plugin does not initiate subscription or credit purchases.

The MCP connection represents a Supademo account and can reach its accessible workspaces. Selecting a workspace for a task does not narrow the token to that workspace or make the connection read-only. Users can revoke the connection through their connected-app/token settings.
