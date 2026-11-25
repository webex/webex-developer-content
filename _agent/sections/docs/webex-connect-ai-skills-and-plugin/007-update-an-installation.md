---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Complete the task
- Update an installation
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin). [Full Markdown](../../../../docs/webex-connect-ai-skills-and-plugin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [MCP endpoints, region, and authentication](009-mcp-endpoints-region-and-authentication.md)

## Article introduction

Install and use Webex Connect AI Skills with Codex, Claude Code, Cursor, or standalone skill packages. This guide explains the 19 available skills, plugin and skill installation, tenant and credential prerequisites, common workflows, MCP setup, and production safeguards.

## Parent context

## Complete the task

## Selected section

### Update an installation

Before updating, close active sessions using Webex Connect AI. After updating, restart or reload the host so it does not keep an older copy in memory. Updating a plugin or skill does not change the tenant, digital assets, sender IDs, project `.env`, or secure MCP credentials.

For a Codex Git-backed marketplace, refresh the source:

```bash
codex plugin marketplace upgrade webex-skills
```

Open `/plugins` in Codex to inspect Webex Connect AI and use the available plugin update action. If no update is offered, remove and reinstall the plugin from the refreshed **Webex Skills** marketplace. Start a new Codex session after updating.

For Claude Code, update the marketplace and plugin:

```text
/plugin marketplace update webex-skills
```

Or use the CLI:

```bash
claude plugin marketplace update webex-skills
claude plugin update webex-connect-ai@webex-skills
claude plugin list
```

For the local Cursor installation, update the `webex-skills` clone used during installation and copy the refreshed plugin files into Cursor's local plugin directory:

```bash
git pull --ff-only
rsync -a --delete ./plugin-packages/webex-connect-ai/ ~/.cursor/plugins/local/webex-connect-ai/
```

The trailing slashes copy the package contents, and `--delete` removes local files that are no longer in the source. Reload Cursor and confirm the updated skills, commands, and rules are visible.

To update a standalone skill, rerun its installer with the same client and scope and add `--force`. For example:

```bash
npx --yes \
  --package https://raw.githubusercontent.com/webex/webex-skills/main/skills/webexconnect-sms-sendmessage/release/webexconnect-sms-sendmessage-latest.tgz \
  webexconnect-sms-sendmessage install --client codex --scope user --force
```

Review local modifications before replacing a skill. For project installs, run from the target project and keep `--scope project`. Do not mix skill directories from different releases.
