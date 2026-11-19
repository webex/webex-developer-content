---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-operation-mcp-server
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Tools
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-operation-mcp-server). [Full Markdown](../../../../docs/contact-center-operation-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](004-authentication.md) [Scopes](005-scopes.md)

## Selected section

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
