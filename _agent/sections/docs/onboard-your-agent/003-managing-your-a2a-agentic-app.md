---
type: Excerpt
canonical_url: https://developer.webex.com/docs/onboard-your-agent
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Managing Your A2A Agentic App
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/onboard-your-agent). [Full Markdown](../../../../docs/onboard-your-agent.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

---

This guide helps developers register an A2A (Agent2Agent) Agentic App on the [Webex Developer Portal](https://developer.webex.com/my-apps/new).

A2A is an open communication standard that enables multiple agents — potentially using different LLMs, runtimes, or toolsets — to exchange messages, delegate tasks, and collaborate. Unlike MCP, which connects one agent to external capabilities, A2A connects multiple agents to each other.

> **Beta**: A2A registration is currently available only in beta. You must sign up for the [beta program](https://developer.webex.com/mcp/docs/webex-developer-beta-program) to access this feature.

## Selected section

## Managing Your A2A Agentic App

From the details page, you can:

- View app ID and configuration.
- Edit name, description, and logo.
- View transport type and auth type (read-only, sourced from the Agent Card).
- Submit a request to make the app public on the Webex App Hub.
- Request admin approval for org/user level use.
- Delete the app.

> **Note**: Transport type and auth type cannot be edited for A2A apps — they are managed by the Agent Card at your server's well-known URL. Server URL is also non-editable after registration since it drives the Agent Card discovery.
