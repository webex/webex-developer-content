---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Security and operational guidance
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin). [Full Markdown](../../../../docs/webex-connect-ai-skills-and-plugin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [MCP endpoints, region, and authentication](009-mcp-endpoints-region-and-authentication.md)

## Article introduction

Install and use Webex Connect AI Skills with Codex, Claude Code, Cursor, or standalone skill packages. This guide explains the 19 available skills, plugin and skill installation, tenant and credential prerequisites, common workflows, MCP setup, and production safeguards.

## Selected section

## Security and operational guidance

- Review the plugin source and manifest before installing, especially from a third-party marketplace.
- Grant filesystem and MCP permissions only to workflows that need them.
- Keep secrets in an ignored local `.env` with owner-only access or in the host's secure credential store. Never paste bearer tokens or Service Keys into a public prompt, README, issue, generated source, or committed environment file.
- Use test recipients and assets before Production sends.
- Confirm the environment, tenant, sender, recipient, and payload before each irreversible action.
- Configure Contact Policy and opt-out handling for promotional messages.
- Treat API acceptance, provider delivery, and end-user display as separate states.
