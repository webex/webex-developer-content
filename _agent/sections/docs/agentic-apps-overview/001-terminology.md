---
type: Excerpt
canonical_url: https://developer.webex.com/docs/agentic-apps-overview
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Terminology
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/agentic-apps-overview). [Full Markdown](../../../../docs/agentic-apps-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Learn the key concepts, terminology, and components of agentic apps and the Model Context Protocol (MCP) for building AI-powered integrations.

---

This guide introduces the foundational concepts behind agentic apps and the Model Context Protocol (MCP), including key terminology, server capabilities, and schema definitions.

## Selected section

## Terminology

**Agentic App** - An Agentic App is a service that exposes structured capabilities, such as actions, data sources, or prompts, that an AI agent can invoke to perform tasks. It is not tied to a specific protocol but is analogous to an MCP server when using the MCP standard.

**MCP** - MCP (Model Context Protocol) is an open standard enabling LLMs to discover and use external data and tools. It provides a standardized way for AI agents to access server capabilities without custom integrations.

**Agents** - An AI agent is a software program that can autonomously perform tasks on behalf of a user by using reasoning, planning, and action to achieve goals. It typically consists of code and one or more prompts and interacts with one or more LLMs to perform its function.

**User** – The user who interacts with the agent to perform a task. The user may invoke specific actions, fetch and attach resources to the context used by the agent, and provide consent to risky interactions. A user may not be present in all agent interactions.

**MCP Server** - A server program that exposes tools, resources, prompts, and configuration of metadata using the MCP specification. It acts as the provider of capabilities that the LLM can invoke.

**MCP Client** - A component, often embedded in the agent runtime or AI application, that discovers MCP servers, reads their capability metadata, validates schemas, and sends execution requests to them. It acts as the consumer side of MCP.

**A2A** - A2A (Agent2Agent) is an open communication standard that enables multiple agents potentially using different LLMs, runtimes, or toolsets to exchange messages, delegate tasks, and collaborate. Unlike MCP, which connects one agent to external capabilities, A2A connects multiple agents to each other.
