---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-operation-mcp-server-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 6. Test one contact and related artifacts
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-operation-mcp-server-beta). [Full Markdown](../../../../docs/contact-center-operation-mcp-server-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test the Webex Contact Center Operation MCP Server with a supported MCP client during the Webex Developer Beta. For the complete tool reference, see [Contact Center Operation MCP Server](https://developer.webex.com/docs/contact-center-operation-mcp-server).

## Selected section

## 6. Test one contact and related artifacts

Use an approved test contact or task ID. Do not include the customer's phone number, address, transcript, or other sensitive content in the test report.

| Check | Operations MCP tool | What to validate |
|---|---|---|
| Contact journey | `wxcc-operations-get-contact-timeline` | The contact's arrival, IVR, queue, agent, transfer, hold, wrap-up, and termination events are shown in order when available. |
| Contact summaries | `wxcc-operations-get-contact-summaries` | An AI-generated contact summary is returned for the approved contact when available. |
| Recording metadata | `wxcc-operations-list-recordings` | Recording and transcript metadata is listed for the approved contact. |
| Virtual Agent summary | `wxcc-operations-get-va-summary` | The approved contact's Virtual Agent handoff or reconnect summary is returned when available and authorized. |
| Virtual Agent transcript | `wxcc-operations-get-va-transcript` | The approved contact's Virtual Agent transcript is returned when available, authorized, and the tenant has the required entitlement. |

Operations MCP recording checks are metadata checks. They are not a test of playing, downloading, or streaming call or screen recordings. Virtual Agent transcript text is a separate capability and should be tested only with approved contacts, the `cjp:user` scope, and the required entitlement.

### Contact pass criteria

- The selected contact or task is the one being tested.
- Events are presented in chronological order when available.
- Contact-level, session-level, and leg-level information is not mixed without explanation.
- Missing, delayed, or partial artifacts are identified.
- No recording media or unnecessary customer content is exposed.
