---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin). [Full Markdown](../../../../docs/webex-connect-ai-skills-and-plugin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [MCP endpoints, region, and authentication](009-mcp-endpoints-region-and-authentication.md)

## Article introduction

Install and use Webex Connect AI Skills with Codex, Claude Code, Cursor, or standalone skill packages. This guide explains the 19 available skills, plugin and skill installation, tenant and credential prerequisites, common workflows, MCP setup, and production safeguards.

## Selected section

## Troubleshooting

### A skill is not discovered

Confirm that the selected skill is installed in the correct host or project skills directory, that its folder contains `SKILL.md`, and that the directory uses the expected skill name. Reload or restart the AI tool.

### The plugin is installed but its commands are missing

Check that the installed plugin package contains its manifests, `skills/`, `commands/`, and `rules/` directories. For local installs, confirm the plugin path points to `plugin-packages/webex-connect-ai/`, then reload the host.

### Sandbox setup asks for MCP authentication

Stop and confirm the selected environment. Sandbox does not use the Production CPaaS MCP server or its credentials.

### Sender discovery returns no compatible sender

Do not invent a sender ID. Ask the tenant administrator to approve or expose a sender for the intended channel and use case, then repeat discovery.

### A message is queued but not received

Queued means accepted for processing, not delivered. Check the recipient or device registration, sender configuration, channel credentials, provider status, webhook receipts, and tenant logs.
