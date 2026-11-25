---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Authentication
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-agentic-mcp-servers). [Full Markdown](../../../../docs/webex-agentic-mcp-servers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide helps developers integrate Webex MCP (Model Context Protocol) servers with popular AI clients. MCP enables AI agents to securely access Webex capabilities through the Model Context Protocol.

## Selected section

## Authentication

Webex MCP servers support two authorization methods: Token-Based authentication and OAuth 2.0. Please verify the required authentication approach before generating the token.

### 1. Token-Based Authentication

Use a WCIT (Webex Client Identity Token) to authenticate with Webex MCP servers. The WCIT is issued with only the `spark:mcp` scope which will allow to connect to MCP server. Additional scopes required by specific tools are requested at runtime via MCP elicitation during too call.

> **Note**: This method only works with clients that support MCP elicitation. If your client does not support elicitation, use OAuth 2.0 instead.
>
> **What is MCP elicitation?** Elicitation is a capability in the MCP protocol that allows an MCP server to request additional information from the user during a tool call — for example, prompting the user to grant consent for specific OAuth scopes. When using a WCIT token, the initial connection uses only the `spark:mcp` scope. When a tool requires additional scopes (e.g., `meeting:schedules_read`), the server uses elicitation to ask the user to authorize those scopes in real time. Clients that support elicitation can handle this flow seamlessly; clients that do not will fail on tools requiring additional scopes.

1. Navigate to the [Generate WCIT Token](https://developer.webex.com/agentic-token) page in the Webex Developer Portal
2. Enter an appropriate name for your token
3. Click **Generate New Token**
4. Copy the generated token and store it securely (you'll need this for configuration)

> **Important**: Keep your token secure and never commit it to version control.

### 2. OAuth 2.0

OAuth 2.0 can be used by clients that do not support elicitation. This requires creating a Webex Integration with the appropriate scopes.

1. Navigate to the [Create a New Integration](https://developer.webex.com/my-apps/new/integration) page
2. Fill in the form:
   - **Will this integration use a mobile SDK?** No
   - **Integration name:** Give any name
   - **Icon:** Choose one of the default icons
   - **App Hub Description:** Give any description
   - **Redirect URI(s):** You'll get this from the OAuth configuration page in your client
   - **Scopes:** Select the scopes required by your MCP server along with `spark:mcp`. To find the required scopes, go to the [Agentic Apps](https://apphub.webex.com/agentic-apps) page, choose your server, and click **Learn More** to open the MCP Server product page in Developer Portal where the required scopes are listed.
5. Click **Add Integration** to create your integration
6. On the following screen note down the **Client ID** and **Client Secret** — you won't be able to read your Client Secret again once you leave this page
