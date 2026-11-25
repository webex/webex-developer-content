---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-agentic-mcp-servers). [Full Markdown](../../../../docs/webex-agentic-mcp-servers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](002-authentication.md)

## Article introduction

This guide helps developers integrate Webex MCP (Model Context Protocol) servers with popular AI clients. MCP enables AI agents to securely access Webex capabilities through the Model Context Protocol.

## Selected section

## Troubleshooting

### Common Issues

#### Connection Failed

**Problem**: MCP server fails to connect

**Solutions**:
- Verify your WCIT token is valid and not expired
- Check that the endpoint URL is correct
- Ensure you have an active internet connection

#### Authentication Error

**Problem**: "401 Unauthorized" or authentication errors

**Solutions**:
- Regenerate your WCIT token from the Developer Portal
- Ensure the token is properly formatted with "Bearer " prefix in the configuration
- Check that the token hasn't been revoked

#### Server Not Responding

**Problem**: MCP server is not responding to requests

**Solutions**:
- Verify your firewall isn't blocking the connection
- Try restarting your AI client

#### Tools Not Appearing

**Problem**: Webex tools don't show up in the AI client

**Solutions**:
- Confirm the configuration file syntax is correct (valid JSON)
- Restart the AI client completely
- Check the AI client's console/logs for error messages
- Verify you're using the latest version of your AI client:
  - **Claude Desktop**: Check for updates via Claude menu > "Check for Updates..."
  - **VS Code**: Ensure GitHub Copilot extension is up to date
  - **Cursor**: Check for IDE updates in Cursor settings

### Getting Help

If you continue to experience issues, visit the [Webex Developer Support](https://developer.webex.com/explore/support).
