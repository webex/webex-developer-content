---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-copilot-studio
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- OAuth Configuration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-agentic-mcp-servers-copilot-studio). [Full Markdown](../../../../docs/webex-agentic-mcp-servers-copilot-studio.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

This guide walks you through how you can connect your agent in Copilot Studio to Webex MCP server.

> Before configuring, you'll need OAuth 2.0 credentials. See [OAuth 2.0 setup instructions](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20) in the main guide.

## Selected section

## OAuth Configuration

Fill in the required fields — **Client ID** and **Client secret** are from your [Webex OAuth 2.0 Integration](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20):

- **Client ID**
- **Client secret**
- **Authorization URL:** `https://webexapis.com/v1/authorize`
- **Token URL template:** `https://webexapis.com/v1/access_token`
- **Refresh URL:** `https://webexapis.com/v1/access_token`
- **Scopes:** The permissions your app is asking for, as a space-separated list

Select **Create** to add the server. A callback URL appears.

Copy the callback URL to add to your application's registration when creating your Webex OAuth 2.0 Integration.

Select **Next** to continue.
