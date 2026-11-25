---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-cursor
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Method 2: OAuth flow'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-agentic-mcp-servers-cursor). [Full Markdown](../../../../docs/webex-agentic-mcp-servers-cursor.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

Connect Cursor to a Webex MCP server using token-based authentication with one-click install, or via OAuth.

## Selected section

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
