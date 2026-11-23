---
type: Excerpt
canonical_url: https://developer.webex.com/docs/agentic-apps-overview
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- What an MCP Server Provides
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/agentic-apps-overview). [Full Markdown](../../../../docs/agentic-apps-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Learn the key concepts, terminology, and components of agentic apps and the Model Context Protocol (MCP) for building AI-powered integrations.

---

This guide introduces the foundational concepts behind agentic apps and the Model Context Protocol (MCP), including key terminology, server capabilities, and schema definitions.

## Selected section

## What an MCP Server Provides

MCP servers expose capabilities (also called functions) that AI agents can discover and invoke:

**Tools** - Executable actions exposed by the server that the LLM can invoke via an MCP client. A tool typically has an input schema that represents arguments the agent can provide, and an output schema which represents the structure of the returned result. Tools behave like RPC functions, API calls, or commands.

**Resources** - Read-only data entities such as documents, configurations, or database-backed views, that an agent or a user can request or subscribe to for context.

**Prompts** - Structured, reusable instruction templates provided by the server to help the agent instruct the LLM to perform specific tasks. Prompts may include placeholders that can be populated by the agent based on the context or user input.

**Custom Parameters** - Additional configuration values which the user can provide to the MCP client so that it can connect to an MCP server.
