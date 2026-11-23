---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Managing Your MCP Connection
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-agentic-mcp-servers). [Full Markdown](../../../../docs/webex-agentic-mcp-servers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](002-authentication.md)

## Article introduction

This guide helps developers integrate Webex MCP (Model Context Protocol) servers with popular AI clients. MCP enables AI agents to securely access Webex capabilities through the Model Context Protocol.

## Selected section

## Managing Your MCP Connection

### Unlinking an MCP Server

If you need to remove an MCP server from your AI client:

**Claude Desktop:**
1. Open Settings > Developer tab
2. Click "Edit Config" to open `claude_desktop_config.json`
3. Remove the server entry from the `mcpServers` object
4. Save the file and restart Claude Desktop

**VS Code:**
1. Use Command Palette: **MCP: Remove Server** and select the server to remove, or
2. Manually edit `mcp.json` (global or workspace) and remove the server entry from the `servers` object
3. Reload the VS Code window

**Cursor IDE:**
1. Open Cursor Settings > Tools & Integrations > MCP Tools
2. Remove the server entry from `~/.cursor/mcp.json`
3. Save the file (Cursor will automatically detect the change)

### Revoking Your WCIT Token

If your token is compromised or you no longer need it:

1. Navigate to the **Manage WCIT Tokens** page in the Webex Developer Portal
2. Locate the token you want to revoke in the list
3. Click the **Delete** button next to the token
4. Confirm the revocation

> **Important**: After revoking a token, any AI clients using that token will immediately lose access to Webex MCP servers. You'll need to generate a new token and update your client configurations.
