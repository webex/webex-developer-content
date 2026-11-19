---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-gemini-cli
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-agentic-mcp-servers-gemini-cli). [Full Markdown](../../../../docs/webex-agentic-mcp-servers-gemini-cli.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

Connect Gemini CLI to a Webex MCP server.

> Before configuring, you'll need OAuth 2.0 credentials. See [OAuth 2.0 setup instructions](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20) in the main guide.

## Selected section

## Troubleshooting

### MCP server is blocked

If you see an error indicating that the MCP server is blocked, you need to add the server name to the `mcp.allowed` list in `~/.gemini/settings.json`:

```javascript
{
  "mcp": {
    "allowed": [
      "your-server-name"
    ],
    "excluded": []
  }
}
```

Add the exact server name you used in `mcpServers` to the `allowed` array, then restart Gemini CLI.
