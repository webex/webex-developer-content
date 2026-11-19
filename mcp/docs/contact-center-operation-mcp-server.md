---
type: Guide
title: Webex MCP Server | Contact Center Operation MCP Server
display_title: Contact Center Operation MCP Server
canonical_url: https://developer.webex.com/docs/contact-center-operation-mcp-server
content_type: documentation
product_group:
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/contact-center-operation-mcp-server)

## What is Contact Center Operation MCP Server?

The Webex Contact Center Operation MCP Server brings Webex Contact Center operational data and configuration into AI assistants, so teams can investigate live operations using natural language instead of manually stitching together reports, configuration screens, flow exports, recordings, and AI Agent data.

It is designed for contact center teams that need faster, evidence-based answers to operational questions:

- Why did a customer reach a specific queue?
- Which queues are driving transfers, consults, or conferences?
- What happened before a call reached an agent?
- Which flows, queues, skills, or agents are involved in a routing issue?
- How are AI Agents and Virtual Agents performing?
- Which contacts have summaries, transcripts, recordings, or AI insights?

The value is not just access to data. The value is context. The MCP server gives the assistant structured access to Webex Contact Center for reporting, agent activity, configuration, routing, flow definitions, contact journeys, recordings, and AI data so it can reason from tenant-grounded evidence rather than guess.

This helps supervisors, administrators, analysts, support teams, and solution engineers reduce investigation time, validate routing behavior, understand customer journeys, and explain contact center outcomes more clearly.

> **Prerequisites:** This MCP server must be enabled by your organization's admin in Webex Control Hub before it can be used.



> MCP server availability and your organization's endpoint require sign-in on the [official portal page](<https://developer.webex.com/docs/contact-center-operation-mcp-server>).



## Tools

25 tools covering reporting, configuration, flows, routing, contact journey, recordings, and AI Agent and Virtual Agent data:

### Reporting & Search (5)

| Tool | Description |
|------|-------------|
| `wxcc-operations-describe-metrics` | Discovers supported Agent Report metrics and Contact Report measures, dimensions, filters, formulas, enums, and limits. |
| `wxcc-operations-generate-report` | Generates historical contact, queue, and leg analytics from Contact Session Record and Contact Leg Record data. |
| `wxcc-operations-generate-agent-report` | Generates historical agent reporting from Agent Session Record and Agent Activity Record data. |
| `wxcc-operations-run-search-query` | Runs a raw GraphQL query against the Webex Contact Center Search API and returns rows or aggregations. |
| `wxcc-operations-validate-schema` | Validates the reporting catalog against the tenant's live Search API schema. |

### Configuration (4)

| Tool | Description |
|------|-------------|
| `wxcc-operations-describe-org` | Describes tenant-level Contact Center configuration using authoritative totals and bounded samples. |
| `wxcc-operations-list-config` | Lists supported configuration resources with authoritative totals, bounded rows, and explicit coverage. |
| `wxcc-operations-get-config-object` | Retrieves a supported configuration object by ID with bounded, status-aware enrichment. |
| `wxcc-operations-get-configuration-references` | Lists bounded incoming references to a supported configuration object. |

### Flows (2)

| Tool | Description |
|------|-------------|
| `wxcc-operations-list-flows` | Lists configured Flow Designer flows and the entry points bound to each flow. |
| `wxcc-operations-export-flow` | Exports a read-only flow definition for inspecting activities, integrations, variables, and routing logic. |

### Routing & Staffing (3)

| Tool | Description |
|------|-------------|
| `wxcc-operations-explain-queue-routing` | Explains a queue's routing model, skill requirements and sources, agent coverage, and routing dependencies. |
| `wxcc-operations-get-agent-activity` | Retrieves one agent's state history or latest per-channel state within a bounded window. |
| `wxcc-operations-get-agents-by-skill` | Finds agents configured with a skill through their assigned skill profiles. |

### Contacts & Recordings (3)

| Tool | Description |
|------|-------------|
| `wxcc-operations-get-contact-timeline` | Reconstructs one contact's lifecycle or recorded flow milestones from its Contact Activity Record. |
| `wxcc-operations-get-contact-summaries` | Retrieves Cisco AI Assistant-generated contact summaries where available. |
| `wxcc-operations-list-recordings` | Lists call, screen recording, and transcript metadata for contacts without retrieving media. |

### AI & Virtual Agents (8)

| Tool | Description |
|------|-------------|
| `wxcc-operations-get-ai-features` | Shows the tenant's Cisco AI Assistant feature configuration and scope. |
| `wxcc-operations-list-ai-agents` | Counts, lists, searches, or summarizes AI Agents configured in AI Agent Studio. |
| `wxcc-operations-audit-ai-agent` | Runs a bounded configuration, exact-session, or recent-sample audit of one AI Agent. |
| `wxcc-operations-list-ai-agent-sessions` | Counts, lists, or summarizes a bounded session population for one AI Agent. |
| `wxcc-operations-get-ai-agent-session` | Retrieves metadata for exactly one AI Agent session. |
| `wxcc-operations-get-ai-agent-session-messages` | Counts or retrieves bounded messages and observed tool activity for one AI Agent session. |
| `wxcc-operations-get-va-summary` | Retrieves the AI-generated Virtual Agent handoff or reconnect summary for one contact. |
| `wxcc-operations-get-va-transcript` | Retrieves the Virtual Agent transcript for one contact. Requires appropriate scope and entitlement because it can expose conversation content. |

## Connect to your MCP Client

Select your AI client to get connection instructions:

- [Amazon Quick](https://developer.webex.com/docs/webex-agentic-mcp-servers-amazon-quick)
- [Claude Code](https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-code)
- [Claude Desktop](https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-desktop)
- [Codex](https://developer.webex.com/docs/webex-agentic-mcp-servers-codex)
- [Copilot Studio](https://developer.webex.com/docs/webex-agentic-mcp-servers-copilot-studio)
- [Cursor](https://developer.webex.com/docs/webex-agentic-mcp-servers-cursor)
- [Gemini CLI](https://developer.webex.com/docs/webex-agentic-mcp-servers-gemini-cli)
- [VS Code](https://developer.webex.com/docs/webex-agentic-mcp-servers-vscode)

## Authentication

**Auth Type:** OAuth 2.0 Bearer Token

**Issuer:** `https://idbroker.webex.com`

**Flow:** The MCP client obtains a Webex OAuth token and passes it via the `Authorization: Bearer <token>` header. The server validates organization access and forwards the token to Webex Contact Center APIs on behalf of the authenticated user.

## Scopes

4 OAuth scopes required:

| Scope | Description |
|-------|-------------|
| `spark:mcp` | Required to connect through the Webex MCP server platform. |
| `cjp:config_read` | Read access to Webex Contact Center configuration and reporting-related APIs. |
| `spark:people_read` | Read access to Webex identity information used for organization and agent resolution. |
| `cjp:user` | Required for selected Virtual Agent insight APIs, including VA transcript and VA summary access. |

**Full scope string:**

```sh
spark:mcp cjp:config_read spark:people_read cjp:user
```
