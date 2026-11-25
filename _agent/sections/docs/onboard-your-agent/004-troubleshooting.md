---
type: Excerpt
canonical_url: https://developer.webex.com/docs/onboard-your-agent
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting
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

## Troubleshooting

| Error | Cause | Solution |
|-------|-------|----------|
| "This A2A server is not supported" | Agent Card missing required fields, no supported interface (1.x), or no mappable security scheme | Verify your Agent Card conforms to the A2A 1.x spec and includes at least one supported interface and security scheme |
| "Could not fetch Agent Card from the A2A server" | Server unreachable, DNS failure, timeout, or HTTP error | Verify the server is running, reachable over HTTPS, and serves the Agent Card at `/.well-known/agent-card.json` |
| "serverUrl must be a base URL with no path segments" | URL contains path segments (e.g., `/api/v1`) | Provide only the base URL (e.g., `https://agent.example.com`) |
