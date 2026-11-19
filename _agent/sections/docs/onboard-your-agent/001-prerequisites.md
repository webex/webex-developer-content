---
type: Excerpt
canonical_url: https://developer.webex.com/docs/onboard-your-agent
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Prerequisites
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/onboard-your-agent). [Full Markdown](../../../../docs/onboard-your-agent.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

This guide helps developers register an A2A (Agent2Agent) Agentic App on the [Webex Developer Portal](https://developer.webex.com/my-apps/new).

A2A is an open communication standard that enables multiple agents — potentially using different LLMs, runtimes, or toolsets — to exchange messages, delegate tasks, and collaborate. Unlike MCP, which connects one agent to external capabilities, A2A connects multiple agents to each other.

> **Beta**: A2A registration is currently available only in beta. You must sign up for the [beta program](https://developer.webex.com/mcp/docs/webex-developer-beta-program) to access this feature.

## Selected section

## Prerequisites

Before starting, ensure you have:

- Access to the Webex Developer Portal.
- Enrollment in the **[A2A beta program](https://developer.webex.com/mcp/docs/webex-developer-beta-program)**.
- A deployed A2A server reachable via HTTPS.
- An Agent Card served at `{serverUrl}/.well-known/agent-card.json` conforming to [A2A Protocol v1.x](https://a2a-protocol.org/latest/specification/).

> A2A authentication and transport details are auto-discovered from your server's Agent Card — you do not need to provide them manually during registration.

### Agent Card Requirements

Your Agent Card must include:

- **`supportedInterfaces`** — at least one interface with `protocolVersion` 1.x (1.0–1.9).
- **`securitySchemes`** — at least one supported scheme:
  - `oauth2SecurityScheme` (authorization code or client credentials flow)
  - `apiKeySecurityScheme`
- A valid `name` and `description` (optional but recommended for pre-populating the form).

The `serverUrl` you provide must be a **base URL with no path segments** (e.g., `https://agent.example.com`). The portal appends `/.well-known/agent-card.json` automatically.
