---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-vscode
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Method 1: Token-based (WCIT)'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-agentic-mcp-servers-vscode). [Full Markdown](../../../../docs/webex-agentic-mcp-servers-vscode.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

Connect VS Code (GitHub Copilot) to a Webex MCP server using token-based authentication with one-click install, or via OAuth.

## Selected section

## Method 1: Token-based (WCIT)

> VS Code with GitHub Copilot supports MCP elicitation, so you can authenticate with a WCIT token. Additional OAuth scopes required by specific tools are requested at runtime during tool calls — no integration setup needed.

### Generate WCIT Token

Generate a WCIT token to connect using token-based authentication. The WCIT is issued with only the `spark:mcp` scope, which allows you to connect to the MCP server. Additional scopes required by specific tools are requested at runtime via MCP elicitation during tool calls.

[Generate Token](<https://developer.webex.com/agentic-token>)

### Install

Paste your WCIT token and click **Install**.



To configure the MCP connection for your account, open the [official portal page](<https://developer.webex.com/docs/webex-agentic-mcp-servers-vscode>) and sign in.



After installing, click the **Manage** button and select **Start Server** to connect.
