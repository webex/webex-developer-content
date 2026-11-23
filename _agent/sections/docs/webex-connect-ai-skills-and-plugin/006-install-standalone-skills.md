---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Complete the task
- Install standalone skills
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin). [Full Markdown](../../../../docs/webex-connect-ai-skills-and-plugin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [MCP endpoints, region, and authentication](009-mcp-endpoints-region-and-authentication.md)

## Article introduction

Install and use Webex Connect AI Skills with Codex, Claude Code, Cursor, or standalone skill packages. This guide explains the 19 available skills, plugin and skill installation, tenant and credential prerequisites, common workflows, MCP setup, and production safeguards.

## Parent context

## Complete the task

## Selected section

### Install standalone skills

Choose a skill from the catalog and install its package. The packages are distributed as GitHub archives; they do not need to be published to the npm registry. Installers use `npx`.

For example, install the SMS skill for Codex at user scope:

```bash
npx --yes \
  --package https://raw.githubusercontent.com/webex/webex-skills/main/skills/webexconnect-sms-sendmessage/release/webexconnect-sms-sendmessage-latest.tgz \
  webexconnect-sms-sendmessage install --client codex --scope user
```

Install the setup skill as well when you plan to use API-backed workflows:

```bash
npx --yes \
  --package https://raw.githubusercontent.com/webex/webex-skills/main/skills/webex-connect-setup/release/webex-connect-setup-latest.tgz \
  webex-connect-setup install --client codex --scope user
```

Use `--scope project` to install into the current application project. Installer-supported clients include Codex, Claude Code, and GitHub Copilot; `--client all` installs for Codex, GitHub Copilot, and Claude Code. Check the selected skill's package metadata for the supported clients.
