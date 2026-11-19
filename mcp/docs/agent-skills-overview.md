---
type: Guide
title: Agent Skills | Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/agent-skills-overview
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/agent-skills-overview)

**Agent Skills** package reusable instructions and resources that guide AI agents through common Webex tasks. Learn how skills work with agents and Webex MCP servers.

## Agent Skills Overview

An agent is an AI-powered application that interprets a user's request, determines the steps needed to complete it, and selects the appropriate knowledge, skills, and tools. Agents can support users directly in a conversation or work behind the scenes as part of an automated workflow.

In Webex, agents can help people collaborate, communicate, and manage work across meetings, messaging, calling, contact center, and administrative experiences.

## What is an Agent Skill?

An Agent Skill is a reusable set of instructions and resources that gives an agent specialized knowledge or a repeatable way to complete a task.

A skill describes:

- The task or scenario it supports.
- When the agent should use it.
- The steps the agent should follow.
- The tools or information required.
- The expected result and relevant constraints.

Skills complement tools. A tool provides an operation that an agent can perform, while a skill guides the agent in deciding when and how to use one or more tools to complete a workflow.

## Agent Skills and Webex MCP Servers

Webex MCP servers expose Webex capabilities as tools that compatible agents can discover and invoke. Agent Skills can provide the task-specific guidance needed to combine these tools into useful Webex workflows.

A typical interaction follows this pattern:

1. A user describes the outcome they want.
2. The agent identifies the appropriate skill.
3. The skill guides the agent in selecting and using the required Webex tools.
4. The agent returns the result or asks for additional information when needed.

For example, Agent Skills could help an agent:

- Prepare a user for an upcoming meeting.
- Find relevant conversation context and create a follow-up.
- Coordinate meeting and messaging activities.
- Assist with contact center workflows.
- Guide administrators through supported Webex tasks.
- Combine Webex capabilities with approved external services.

## Benefits of Agent Skills

Agent Skills make agent behavior easier to extend and manage:

- **Reusable** - Create a skill once and use it with multiple agents.
- **Focused** - Keep each skill centered on a specific task or outcome.
- **Consistent** - Provide repeatable guidance for common Webex workflows.
- **Composable** - Combine skills and tools to support more complex requests.
- **Discoverable** - Help agents select the right capability for a user's request.
- **Controlled** - Keep actions subject to the permissions and policies of Webex and connected services.

By combining agents, Agent Skills, and Webex MCP servers, developers can create natural-language experiences that turn user intent into useful, controlled actions across Webex.
