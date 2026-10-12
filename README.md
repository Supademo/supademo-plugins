# Supademo plugins

Provider plugin bundles for creating, personalizing, organizing, and analyzing interactive product demos with Supademo.

## Claude

The [Supademo Claude plugin](claude/README.md) includes 25 workflow skills and a reference to the existing Supademo MCP connector at `https://mcp.supademo.com/mcp`. Connect your Supademo account to use the tools available to your workspace role and plan.

```text
claude/
  .claude-plugin/plugin.json
  .mcp.json
  README.md
  LICENSE
  skills/
```

See the [Claude README](claude/README.md) for account setup, the included workflows, data handling, and support.

## Directory submission source

Use these source settings for the Claude plugin bundle:

- Repository: `https://github.com/Supademo/supademo-plugins`
- Plugin path: `claude`
- Branch: `main`
- Plugin name: `supademo`
- Initial bundle version: `1.0.0`

The bundle is prepared for Claude directory submission. The source repository is public; directory review and publication are separate steps.

## Package updates

This repository holds exported provider bundles. Keep each provider's package in its own folder and update the complete export together for each release. Version the Claude bundle in `claude/.claude-plugin/plugin.json`.

## License

The distributable plugin files are available under the [MIT License](LICENSE). Access to the Supademo service is governed by its [terms](https://supademo.com/terms).
