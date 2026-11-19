---
type: Excerpt
canonical_url: https://developer.webex.com/docs/ai-in-webex
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- MCP is one part of the picture
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/ai-in-webex). [Full Markdown](../../../../docs/ai-in-webex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Learn how Webex supports agentic AI, where Model Context Protocol (MCP) fits, and which connection model to use for your first Webex AI project.

## Selected section

## MCP is one part of the picture

Start with the interaction your solution needs, then choose the matching connection model.

![Webex agentic platform connecting to four integration models: REST APIs and SDKs, webhooks and events, Model Context Protocol, and Agent-to-Agent.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt455963a29b6b8bb6/6a8c653d04c1e83b58f5ff50/ai-in-webex-agentic-platform-themed.png)

| What you want to build | Connection model | Best fit |
|------------------------|------------------|----------|
| An application that directly controls a defined Webex workflow | Webex REST APIs and SDKs | Deterministic application logic, direct requests, and product-specific capabilities |
| Automation that reacts when something happens in Webex | Webhooks and events | Event-driven workflows and notifications |
| An AI agent that discovers and uses approved tools or context | MCP | Natural-language intent and reusable, structured agent tools |
| Specialized agents that exchange work or delegate tasks | Agent-to-Agent (A2A), currently in beta | Agent collaboration across different domains or runtimes |

MCP servers often call REST APIs behind the scenes. A2A connects agents to agents, while MCP connects an agent to capabilities. These models can work together in one solution.
