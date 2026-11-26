---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Complete the task
- Install the bundled plugin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin). [Full Markdown](../../../../docs/webex-connect-ai-skills-and-plugin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [MCP endpoints, region, and authentication](009-mcp-endpoints-region-and-authentication.md)

## Article introduction

Install and use Webex Connect AI Skills with Codex, Claude Code, Cursor, or standalone skill packages. This guide explains the 19 available skills, plugin and skill installation, tenant and credential prerequisites, common workflows, MCP setup, and production safeguards.

## Parent context

## Complete the task

## Selected section

### Install the bundled plugin

Clone the public repository once. Use a directory where you keep development tools, not your application project root:

```bash
git clone https://github.com/webex/webex-skills.git
cd webex-skills
```

The assembled, installable plugin is in `plugin-packages/webex-connect-ai/`. No local build step is required for normal installation.

#### Codex

Add the Webex Skills marketplace to Codex:

```bash
codex plugin marketplace add https://github.com/webex/webex-skills.git \
  --sparse .agents/plugins \
  --sparse plugin-packages/webex-connect-ai
```

Open Codex and run:

```text
/plugins
```

Select **Webex Skills**, choose **Webex Connect AI**, and select **Install plugin**. Complete any prompts, then start a new Codex session and confirm that the plugin appears in the plugin browser.

#### Claude Code

In a Claude Code session, add the public marketplace and install the plugin:

```text
/plugin marketplace add webex/webex-skills
/plugin install webex-connect-ai@webex-skills
```

Review the plugin details and select user, project, or local scope when prompted. Start a new Claude Code session after installation. Use `/plugin` to inspect installed and available plugins.

#### Cursor

Copy the assembled plugin into Cursor's local plugin directory:

```bash
mkdir -p ~/.cursor/plugins/local/webex-connect-ai
rsync -a --delete ./plugin-packages/webex-connect-ai/ ~/.cursor/plugins/local/webex-connect-ai/
```

Reload Cursor, open **Customize**, and confirm that the skills, commands, and rules are visible. Enterprise administrators may need to allow local plugin imports or distribute the plugin through a team marketplace.
