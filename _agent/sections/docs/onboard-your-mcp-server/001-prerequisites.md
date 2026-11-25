---
type: Excerpt
canonical_url: https://developer.webex.com/docs/onboard-your-mcp-server
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Prerequisites
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/onboard-your-mcp-server). [Full Markdown](../../../../docs/onboard-your-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide helps developers register their MCP server on the [Webex Developer Portal](https://developer.webex.com/my-apps/new). For A2A (Agent2Agent) Agentic Apps, see [Onboard Your Agent](https://developer.webex.com/docs/onboard-your-agent).

## Selected section

## Prerequisites

Before starting, ensure you have:

- Access to the Webex Developer Portal.
- A deployed MCP server reachable via HTTPS.
- Decide which authentication methods your app will offer. For methods that require credentials or configuration, have those values ready. **Webex Service App** does not require you to enter a client ID, client secret, or token. You can select one or more of the following methods:
  - **OAuth 2.0 authorization code** – User-level OAuth flow where each user authenticates and grants access individually.
  - **OAuth 2.0 client credentials** – Organization-level OAuth flow using a single set of client credentials on behalf of the organization.
  - **API key** – A single static key issued at the organization level to identify and authorize requests.
  - **User token** – An individual token representing a specific user's identity and session.
  - **Custom header authentication** – Custom authentication headers that can be configured at the organization or user level.
  - **Webex Service App** – Organization-level machine authentication for eligible Webex-hosted MCP servers.
