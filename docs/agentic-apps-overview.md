---
type: Guide
title: Agentic Apps | Overview
display_title: Agentic Apps Overview
canonical_url: https://developer.webex.com/docs/agentic-apps-overview
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- create
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/agentic-apps-overview)

Learn the key concepts, terminology, and components of agentic apps and the Model Context Protocol (MCP) for building AI-powered integrations.

---

This guide introduces the foundational concepts behind agentic apps and the Model Context Protocol (MCP), including key terminology, server capabilities, and schema definitions.

## Terminology

**Agentic App** - An Agentic App is a service that exposes structured capabilities, such as actions, data sources, or prompts, that an AI agent can invoke to perform tasks. It is not tied to a specific protocol but is analogous to an MCP server when using the MCP standard.

**MCP** - MCP (Model Context Protocol) is an open standard enabling LLMs to discover and use external data and tools. It provides a standardized way for AI agents to access server capabilities without custom integrations.

**Agents** - An AI agent is a software program that can autonomously perform tasks on behalf of a user by using reasoning, planning, and action to achieve goals. It typically consists of code and one or more prompts and interacts with one or more LLMs to perform its function.

**User** – The user who interacts with the agent to perform a task. The user may invoke specific actions, fetch and attach resources to the context used by the agent, and provide consent to risky interactions. A user may not be present in all agent interactions.

**MCP Server** - A server program that exposes tools, resources, prompts, and configuration of metadata using the MCP specification. It acts as the provider of capabilities that the LLM can invoke.

**MCP Client** - A component, often embedded in the agent runtime or AI application, that discovers MCP servers, reads their capability metadata, validates schemas, and sends execution requests to them. It acts as the consumer side of MCP.

**A2A** - A2A (Agent2Agent) is an open communication standard that enables multiple agents potentially using different LLMs, runtimes, or toolsets to exchange messages, delegate tasks, and collaborate. Unlike MCP, which connects one agent to external capabilities, A2A connects multiple agents to each other.

## What an MCP Server Provides

MCP servers expose capabilities (also called functions) that AI agents can discover and invoke:

**Tools** - Executable actions exposed by the server that the LLM can invoke via an MCP client. A tool typically has an input schema that represents arguments the agent can provide, and an output schema which represents the structure of the returned result. Tools behave like RPC functions, API calls, or commands.

**Resources** - Read-only data entities such as documents, configurations, or database-backed views, that an agent or a user can request or subscribe to for context.

**Prompts** - Structured, reusable instruction templates provided by the server to help the agent instruct the LLM to perform specific tasks. Prompts may include placeholders that can be populated by the agent based on the context or user input.

**Custom Parameters** - Additional configuration values which the user can provide to the MCP client so that it can connect to an MCP server.

## What is Schema?

**Schema** - A formal description of the structure, data types, and constraints of information exchanged between an MCP server and client.

**Input Schema** - Defines the required and optional arguments a tool accepts, enabling the agent to construct valid tool calls. Ensures type safety and argument validation.

**Output Schema** - Describes the expected structure of data returned by a tool, allowing the agent to parse and act on tool results predictably.

**Annotations** - Metadata fields attached to tools or schemas that extend functionality beyond standard schema defined by MCP or A2A protocol. They can include UI hints, privacy indicators, categorization tags, or execution constraints.

## Additional Resources

- [A2A Documentation](https://a2a-protocol.org/latest/) - The official documentation for the Agent2Agent protocol.
- [MCP Documentation](https://modelcontextprotocol.io/docs/getting-started/intro) - The official documentation for the Model Context Protocol.
