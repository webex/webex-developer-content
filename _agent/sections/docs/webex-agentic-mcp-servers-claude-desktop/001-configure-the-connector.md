---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-desktop
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Configure the Connector
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-desktop). [Full Markdown](../../../../docs/webex-agentic-mcp-servers-claude-desktop.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

Connect Claude Desktop to a Webex MCP server.

> Before configuring, you'll need OAuth 2.0 credentials. See [OAuth 2.0 setup instructions](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20) in the main guide.

## Selected section

## Configure the Connector

1. Launch Claude Desktop and click on your profile icon (or the Claude menu) and select **Settings**
2. In the sidebar, click on the **Connectors** tab
3. Scroll to the bottom and click **Add custom connector**
4. Fill in the details:
   - **Name:** A unique identifier for this client connector (e.g., `My Webex Meeting`) — this can be anything
   - **URL:** The full URL of the Webex MCP server (must start with `https://`)
5. Expand **Advanced settings** and enter your credentials from your [Webex OAuth 2.0 Integration](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20):
   - **Client ID**
   - **Client Secret**

> When creating your Webex OAuth 2.0 Integration, use `https://claude.ai/api/mcp/auth_callback` as the redirect URL.

6. Click **Save** to add the connector
7. Claude Desktop will initiate the OAuth flow — sign in and grant the requested permissions
