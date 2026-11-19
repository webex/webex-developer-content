---
type: Guide
title: Webex MCP Server Usage Guide | VS Code
display_title: VS Code
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-vscode
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-agentic-mcp-servers-vscode)

---

Connect VS Code (GitHub Copilot) to a Webex MCP server using token-based authentication with one-click install, or via OAuth.

## Method 1: Token-based (WCIT)

> VS Code with GitHub Copilot supports MCP elicitation, so you can authenticate with a WCIT token. Additional OAuth scopes required by specific tools are requested at runtime during tool calls — no integration setup needed.

### Generate WCIT Token

Generate a WCIT token to connect using token-based authentication. The WCIT is issued with only the `spark:mcp` scope, which allows you to connect to the MCP server. Additional scopes required by specific tools are requested at runtime via MCP elicitation during tool calls.

[Generate Token](<https://developer.webex.com/agentic-token>)

### Install

Paste your WCIT token and click **Install**.



To configure the MCP connection for your account, open the [official portal page](<https://developer.webex.com/docs/webex-agentic-mcp-servers-vscode>) and sign in.



After installing, click the **Manage** button and select **Start Server** to connect.

## Method 2: OAuth via mcp-remote

Connect using a full OAuth flow with `mcp-remote`.

Add the following to your VS Code MCP configuration (`.vscode/mcp.json`):

```json
{
  "servers": {
    "my-server": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "<MCP_SERVER_URL>",
        "<PORT>"
        "--static-oauth-client-info",
        "{\"client_id\":\"<YOUR_CLIENT_ID>\",\"client_secret\":\"<YOUR_CLIENT_SECRET>\"}"
      ],
      "type": "stdio"
    }
  }
}
```

> `<YOUR_CLIENT_ID>` and `<YOUR_CLIENT_SECRET>` are from your [Webex OAuth 2.0 Integration](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20).
>
> `<PORT>` can be any available port on your machine. Make sure to register the matching callback URI (`http://localhost:<PORT>/oauth/callback`) when creating your Webex OAuth 2.0 Integration.
