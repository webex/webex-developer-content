---
type: Guide
title: Webex MCP Server Usage Guide | Cursor
display_title: Cursor
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-cursor
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-agentic-mcp-servers-cursor)

---

Connect Cursor to a Webex MCP server using token-based authentication with one-click install, or via OAuth.

## Method 1: Token-based (WCIT)

> Cursor supports MCP elicitation, so you can authenticate with a WCIT token. Additional OAuth scopes required by specific tools are requested at runtime during tool calls — no integration setup needed.

### Generate WCIT Token

Generate a WCIT token to connect using token-based authentication. The WCIT is issued with only the `spark:mcp` scope, which allows you to connect to the MCP server. Additional scopes required by specific tools are requested at runtime via MCP elicitation during tool calls.

[Generate Token](<https://developer.webex.com/agentic-token>)

### Install

Paste your WCIT token and click **Install**.



To configure the MCP connection for your account, open the [official portal page](<https://developer.webex.com/docs/webex-agentic-mcp-servers-cursor>) and sign in.



## Method 2: OAuth flow

Add the following to your Cursor MCP configuration (`~/.cursor/mcp.json`):

```javascript
{
  "mcpServers": {
    "your-mcp-server": {
      "url": "<MCP_SERVER_URL>",
      "auth": {
        "CLIENT_ID": "<YOUR_CLIENT_ID>",
        "CLIENT_SECRET": "<YOUR_CLIENT_SECRET>",
        "scopes": ["spark:mcp", "required_scope1", "required_scope2"]
      }
    }
  }
}
```

> `CLIENT_ID` and `CLIENT_SECRET` are from your [Webex OAuth 2.0 Integration](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20).

Cursor uses a fixed OAuth redirect URL for all MCP servers — register this as the redirect URI when creating your Webex OAuth 2.0 Integration:

```javascript
cursor://anysphere.cursor-mcp/oauth/callback
```

## Resources

- [Cursor Official Documentation](https://cursor.com/docs/mcp)
