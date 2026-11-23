---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Webhook Payload Schemas
- Common Telephony Payload Fields
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/call-control). [Full Markdown](../../../../docs/call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication and Authorization](002-authentication-and-authorization.md)

## Article introduction

Third-party services integrate with Webex Calling using admin-level APIs and admin-level tokens provided via Service Apps. This guide covers authentication, call control APIs, discovery APIs, telephony webhooks, and interest registration.

## Parent context

## Webhook Payload Schemas

This section provides detailed schema information for each telephony webhook resource.

## Selected section

### Common Telephony Payload Fields

All telephony webhook `data` payloads include:

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `eventTimestamp` | string | Date and time the event was emitted (ISO 8601 format). |
| `actorType` | string | The type of the actor: `PEOPLE`, `PLACE`, `VIRTUAL_LINE`, or `CALL_QUEUE`. |
| `eventType` | string | The specific event type (varies by resource). |

---
