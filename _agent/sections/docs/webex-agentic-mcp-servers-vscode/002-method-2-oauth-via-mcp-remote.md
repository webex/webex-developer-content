---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-vscode
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Method 2: OAuth via mcp-remote'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-agentic-mcp-servers-vscode). [Full Markdown](../../../../docs/webex-agentic-mcp-servers-vscode.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

Connect VS Code (GitHub Copilot) to a Webex MCP server using token-based authentication with one-click install, or via OAuth.

## Selected section

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
