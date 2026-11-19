---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-operation-mcp-server-beta
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- 5. Test reporting and historical analytics
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-operation-mcp-server-beta). [Full Markdown](../../../../docs/contact-center-operation-mcp-server-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test the Webex Contact Center Operation MCP Server with a supported MCP client during the Webex Developer Beta. For the complete tool reference, see [Contact Center Operation MCP Server](https://developer.webex.com/docs/contact-center-operation-mcp-server).

## Selected section

## 5. Test reporting and historical analytics

Use a short, agreed time window and the same time zone when comparing results with another Webex Contact Center report or dashboard.

| Check | Operations MCP tool | What to validate |
|---|---|---|
| Contact reporting | `wxcc-operations-generate-report` | Contact, queue, and contact-leg results use the requested time range and reporting definition. |
| Agent reporting | `wxcc-operations-generate-agent-report` | Agent metrics use the selected agents, interval, time zone, and grouping. |
| Custom Search | `wxcc-operations-run-search-query` | A small custom query returns only authorized historical data. Use this when the typed reports cannot answer the question. |
| Agent activity | `wxcc-operations-get-agent-activity` | A known agent's activity is returned for the selected time window. |

Before comparing numbers, record:

- The time range and time zone.
- The report or record type.
- The filters and grouping.
- Whether the result is at contact, contact-leg, human-agent session, agent activity, or interval level.
- The expected count or result from the comparison view.

### Reporting pass criteria

- The tool uses the requested time window and filters.
- The result states what the number represents.
- The result distinguishes returned rows from the total number of matching records.
- A partial, delayed, or unavailable result is identified.
- The client does not claim that a failed query means there were zero records.
