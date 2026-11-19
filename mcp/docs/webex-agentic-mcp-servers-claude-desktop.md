---
type: Guide
title: Webex MCP Server Usage Guide | Claude Desktop
display_title: Claude Desktop
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-desktop
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-desktop)

---

Connect Claude Desktop to a Webex MCP server.

> Before configuring, you'll need OAuth 2.0 credentials. See [OAuth 2.0 setup instructions](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20) in the main guide.

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

## Resources

- [Claude Desktop Official Documentation](https://modelcontextprotocol.io/docs/develop/connect-remote-servers)
