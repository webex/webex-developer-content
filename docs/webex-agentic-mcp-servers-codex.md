---
type: Guide
title: Webex MCP Server Usage Guide | Codex
display_title: Codex
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-codex
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-agentic-mcp-servers-codex)

---

Connect OpenAI Codex to a Webex MCP server.

## Token-based (WCIT)

> Codex supports MCP elicitation, so you can authenticate with a WCIT token. Additional OAuth scopes required by specific tools are requested at runtime during tool calls — no integration setup needed.

### Generate WCIT Token

Generate a WCIT token to connect using token-based authentication. The WCIT is issued with only the `spark:mcp` scope, which allows you to connect to the MCP server. Additional scopes required by specific tools are requested at runtime via MCP elicitation during tool calls.

[Generate Token](<https://developer.webex.com/agentic-token>)

### Add the MCP server configuration

Open or create your Codex configuration file at `~/.codex/config.toml`. Add an entry for the Webex MCP server:

```toml
[mcp_servers.YOUR_MCP_SERVER_NAME]
enabled = true
url = "YOUR_MCP_SERVER_URL"
http_headers = {"Authorization" = "Bearer YOUR_TOKEN"}
```

Replace `YOUR_TOKEN` with your WCIT token.
