---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Webhook Payload Schemas
- Common Webhook Envelope Fields
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

### Common Webhook Envelope Fields

All telephony webhook payloads share a common envelope structure:

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `id` | string | A unique identifier for the webhook. |
| `name` | string | A user-friendly name for the webhook. |
| `targetUrl` | string | The URL that receives the webhook. |
| `resource` | string | The resource type for the webhook (e.g., `telephony_calls`, `telephony_agent`). |
| `event` | string | Event type: `created`, `updated`, or `deleted`. |
| `orgId` | string | The organization that owns the webhook. |
| `createdBy` | string | The ID of the entity that added the webhook. |
| `appId` | string | The ID of the Webex app that was used to create the webhook. |
| `ownedBy` | string | Indicates if the webhook is owned by the `org` or the `creator`. |
| `status` | string | Status of the webhook. Always `active` for emitted webhooks. |
| `created` | string | Date and time the webhook was created. |
| `actorId` | string | The unique identifier of the entity who caused the webhook to be sent. |
| `data` | object | The event-specific payload (see resource schemas below). |
