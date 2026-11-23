---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-operation-mcp-server-beta
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- 7. Test AI Agent Studio information
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-operation-mcp-server-beta). [Full Markdown](../../../../docs/contact-center-operation-mcp-server-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test the Webex Contact Center Operation MCP Server with a supported MCP client during the Webex Developer Beta. For the complete tool reference, see [Contact Center Operation MCP Server](https://developer.webex.com/docs/contact-center-operation-mcp-server).

## Selected section

## 7. Test AI Agent Studio information

Use an approved AI Agent and session if your beta scope includes these tools.

AI Agent Studio tools return configured-agent, session, message, and audit evidence.

| Check | Operations MCP tool | What to validate |
|---|---|---|
| List AI Agents | `wxcc-operations-list-ai-agents` | Authorized AI Agents can be listed. |
| List sessions | `wxcc-operations-list-ai-agent-sessions` | Sessions for one authorized AI Agent can be listed for the selected view. |
| Read one session | `wxcc-operations-get-ai-agent-session` | One known session can be retrieved. |
| Read messages | `wxcc-operations-get-ai-agent-session-messages` | Messages can be counted or returned within the approved limit. |
| Audit an AI Agent | `wxcc-operations-audit-ai-agent` | The selected scope returns a redacted configuration view or bounded evidence from one exact session or up to three recent sessions. |

Do not confuse AI Agent Studio sessions with Contact Center Search analytics, Virtual Agent transcripts, or a contact's ordinary task record.

### AI Agent pass criteria

- The correct AI Agent and session are selected.
- Results are limited to the authorized organization.
- Message results remain within the agreed scope and limit.
- AI Agent Studio evidence is not presented as Contact Center Search analytics.
- Audit findings state their sample and coverage limits and do not label no-tool or ungrounded turns as confirmed hallucinations.
- The response clearly identifies when no session or message data is available.
