---
type: Guide
title: Webex MCP Server Usage Guide | Claude Code
display_title: Claude Code
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-code
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-code)

---

Connect Claude Code CLI to a Webex MCP server.

> Before configuring, you'll need OAuth 2.0 credentials. See [OAuth 2.0 setup instructions](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20) in the main guide.

## OAuth 2.0

```bash
MCP_CLIENT_SECRET=your-secret claude mcp add --transport http \
  --client-id your-client-id --client-secret --callback-port port \
  your-server-name your-server-url
```

Claude Code uses OAuth 2.0 well-known discovery endpoints for configuration, and scopes are fetched from those discovered endpoints.

Set `callbackPort` to match the callback URI you registered when creating your Webex OAuth 2.0 Integration. Make sure to register the callback URI in this format `http://localhost:PORT/callback`. The port can be any available port — it just needs to match your registered callback URI. If omitted, Claude Code picks a random available port.

You'll get the client-id and client-secret from your [Webex OAuth 2.0 Integration](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20)

> **Replace** the values 
> - `your-secret` with the client secret from Webex OAuth Integration
> - `your-server-name` with a descriptive name (e.g., `my-meeting-server`)
> - `your-server-url` with your MCP server endpoint URL
> - `your-client-id` with the Client ID from Webex OAuth Integration
> - `port` with the port matching your registered redirect URI

## Authenticate

After adding the server, run `/mcp` inside Claude Code. The server will show as **failed** with **not authenticated** status.

1. Select the server from the list
2. Choose **Authenticate**
3. A browser window will open for you to sign in and grant access
4. Once authenticated, the server status will update to connected

## Resources

- [Claude Code Official Documentation](https://code.claude.com/docs/en/mcp)
