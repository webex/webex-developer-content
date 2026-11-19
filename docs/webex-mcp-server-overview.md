---
type: Guide
title: Webex MCP Server | Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/webex-mcp-server-overview
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-mcp-server-overview)

## What is Webex MCP (Model Context Protocol)?

Webex provides MCP servers that enable AI agents to securely access various Webex functionalities through the Model Context Protocol. These servers act as a bridge between your AI client and Webex services, allowing AI agents to perform actions and retrieve information on your behalf.

## Benefits of Webex MCP

### 1. Faster AI Integration

Build Webex-powered AI features in hours instead of weeks with a single MCP server that eliminates repetitive API code and works across all AI platforms.

### 2. Natural Language Control

Enable users to manage Webex through conversational commands like "Schedule our quarterly review" or "Find messages about the product launch" without learning APIs.

### 3. Enterprise Security & Governance

Centralized authentication, granular permissions, and complete audit trails give IT unified control over AI access to Webex collaboration data.

### 4. Cross-Platform Workflows

Connect Webex seamlessly with other tools through standardized MCP, enabling AI to orchestrate complex workflows like "Summarize the meeting and share action items with the team".

## Example Use Cases

- "Schedule a meeting with the engineering team tomorrow at 2pm"
- "Send a summary of this document to the project space"
- "Find all messages from Sarah about the Q2 roadmap"
- AI assistant that manages your Webex communications
- Chatbot that joins meetings and takes notes

## Webex APIs vs MCP

Webex APIs are REST-based HTTP endpoints provided by Cisco Webex that developers call directly from their applications to integrate collaboration features like messaging, meetings, calling and device control. You make standard HTTP requests with authentication tokens to interact with Webex services.

### When to Use Webex APIs

Choose Webex REST APIs when you need:

- **Full Control** — Precise control over every API call and response
- **Performance** — Direct API calls with minimal latency
- **Complex Logic** — Your application has intricate business logic
- **Webhooks** — Real-time event notifications via webhooks
- **Enterprise Applications** — Large-scale solutions that need direct API access for performance and security compliance

**Example use cases:**
- Building a custom collaboration app
- Automated meeting scheduling system
- Enterprise SSO integration
- Real-time presence monitoring dashboard

### When to Use Webex MCP

Choose Webex MCP when you need:

- **AI Integration** — Enable AI agents and LLM platforms to interact with Webex using natural language
- **Rapid Prototyping** — Get started quickly without writing repetitive API integration code
- **Cross-Platform** — Connect Webex to any MCP-compatible AI client with a single configuration

**Example use cases:**
- AI assistant that manages your Webex communications
- Chatbot that schedules meetings and takes notes
- Natural language interface for searching messages and spaces

### Using Both Together

You can combine both approaches. For example:

1. Use Webex APIs for direct, programmatic control and production applications
2. Use MCP to enable AI assistants to interact with Webex through natural language

The choice depends on your use case, technical requirements, and whether AI-powered interactions are central to your application.
