---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Complete the task
- MCP endpoints, region, and authentication
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin). [Full Markdown](../../../../docs/webex-connect-ai-skills-and-plugin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Install and use Webex Connect AI Skills with Codex, Claude Code, Cursor, or standalone skill packages. This guide explains the 19 available skills, plugin and skill installation, tenant and credential prerequisites, common workflows, MCP setup, and production safeguards.

## Parent context

## Complete the task

## Selected section

### MCP endpoints, region, and authentication

Use the Integration endpoint for the tenant's staging or preproduction environment, or the Production endpoint for its confirmed region. Do not guess an endpoint that is not listed.

| Webex Connect region | Production MCP server URL |
| --- | --- |
| ca (AWS Canada) | [https://mcp.ca.webexconnect.io/mcp/cpaas](https://mcp.ca.webexconnect.io/mcp/cpaas) |
| eu (AWS Ireland) | [https://mcp.eu.webexconnect.io/mcp/cpaas](https://mcp.eu.webexconnect.io/mcp/cpaas) |
| uk (AWS London) | [https://mcp.uk.webexconnect.io/mcp/cpaas](https://mcp.uk.webexconnect.io/mcp/cpaas) |
| us (United States) | [https://mcp.us.webexconnect.io/mcp/cpaas](https://mcp.us.webexconnect.io/mcp/cpaas) |
| in (AWS Mumbai) | [https://mcp.in.webexconnect.io/mcp/cpaas](https://mcp.in.webexconnect.io/mcp/cpaas) |
| au (AWS Sydney) | [https://mcp.au.webexconnect.io/mcp/cpaas](https://mcp.au.webexconnect.io/mcp/cpaas) |
| sg (AWS Singapore) | [https://mcp.sg.webexconnect.io/mcp/cpaas](https://mcp.sg.webexconnect.io/mcp/cpaas) |

The MCP server must be enabled by an organization administrator in Webex Control Hub and Webex Connect Tenant Settings. An approved SMS phone number or supported Email asset and an approved AI Agent Messaging use case are also required.

Codex supports token-based authentication with a Webex Client Integration Token (WCIT) that has the `spark:mcp` scope. Store the token as a bearer token in Codex's MCP server configuration; protect the local configuration file. The server requests any additional tool scopes at runtime through MCP elicitation. Cursor supports the same WCIT flow and also OAuth through an Integration App; register Cursor's fixed redirect URI `cursor://anysphere.cursor-mcp/oauth/callback`. Claude Code uses client-based browser OAuth; prepare the Integration App client ID, client secret, and matching callback URI listed above. Keep bearer tokens and client secrets in protected local configuration, never in a prompt or committed file.

- **Codex:** configure the selected URL and WCIT as the Authorization bearer token in Codex's MCP server configuration, then protect the local configuration file.
- **Claude Code:** add the selected URL with `claude mcp add --transport http` using the Integration App client ID, client secret, and registered callback port. Then run `/mcp`, select the server, and choose **Authenticate** to complete browser authorization. See the [Claude Code MCP setup guide](https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-code) for the command and callback details.
- **Cursor:** use the one-click WCIT token flow or configure OAuth through the Integration App flow described in Cursor's MCP guide.

The CPaaS MCP server exposes sender discovery and non-templated SMS and Email messaging. Its tools are `webex-sender-ids`, `webex-sms-message`, and `webex-email-message`. Do not use Production MCP credentials for Sandbox. If your tenant region is not listed, confirm it with your administrator and use documented direct APIs until a supported MCP endpoint is confirmed.

Direct API credentials and MCP credentials are separate and are not interchangeable. Keep the selected tenant and environment in your local setup record without storing credential values there.
