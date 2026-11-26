---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Verify the result
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin). [Full Markdown](../../../../docs/webex-connect-ai-skills-and-plugin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [MCP endpoints, region, and authentication](009-mcp-endpoints-region-and-authentication.md)

## Article introduction

Install and use Webex Connect AI Skills with Codex, Claude Code, Cursor, or standalone skill packages. This guide explains the 19 available skills, plugin and skill installation, tenant and credential prerequisites, common workflows, MCP setup, and production safeguards.

## Selected section

## Verify the result

- Confirm the installed plugin or skill and release in the AI host, then reload or restart the host.
- Ask the agent to list the Webex Connect skills and confirm that the expected workflows are available.
- For API-backed work, run setup as a preflight check and confirm the selected tenant, environment, region, endpoint, and required local credentials.
- For MCP, verify the intended regional URL, secure authentication, and the available sender discovery or messaging tools.
- Start with a test tenant, test asset, or test recipient when possible. Record message IDs, correlation IDs, request timestamps, and acceptance status.
- Treat an accepted or queued response as platform acceptance. Check receipts, callbacks, and tenant logs separately to confirm delivery.
