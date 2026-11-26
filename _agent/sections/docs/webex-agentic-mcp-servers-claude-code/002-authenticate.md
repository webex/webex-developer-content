---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-code
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Authenticate
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-code). [Full Markdown](../../../../docs/webex-agentic-mcp-servers-claude-code.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

Connect Claude Code CLI to a Webex MCP server.

> Before configuring, you'll need OAuth 2.0 credentials. See [OAuth 2.0 setup instructions](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20) in the main guide.

## Selected section

## Authenticate

After adding the server, run `/mcp` inside Claude Code. The server will show as **failed** with **not authenticated** status.

1. Select the server from the list
2. Choose **Authenticate**
3. A browser window will open for you to sign in and grant access
4. Once authenticated, the server status will update to connected
