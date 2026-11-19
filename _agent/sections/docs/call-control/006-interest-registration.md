---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Interest Registration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/call-control). [Full Markdown](../../../../docs/call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication and Authorization](002-authentication-and-authorization.md)

## Article introduction

Third-party services integrate with Webex Calling using admin-level APIs and admin-level tokens provided via Service Apps. This guide covers authentication, call control APIs, discovery APIs, telephony webhooks, and interest registration.

## Selected section

## Interest Registration

Webhook interests enable the emission of Webex Calling webhook events that are not emitted by default, even when a webhook is registered for an applicable resource. Clients manage webhook interests through registrations. Once a client registers an interest, that interest applies to all applicable webhooks for the organization, not only webhooks created by that client. Webhook interests are therefore not intended to filter unwanted events.

Webhook interest registrations expire and should be refreshed periodically. The default expiration period is 60 days.

There are two types of webhook interests: **resource interests** and **actor interests**. Webhook events for actor and resource categories without a corresponding interest type do not require an interest registration and are always emitted.

Although POST and DELETE operations are technically "write" operations, they are exceptionally associated with the `spark-admin:calls_read` scope because they are used alongside the read-only Webhook APIs.

### API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/telephony/webhookInterestRegistrations` | Create or update a webhook interest registration |
| GET | `/telephony/webhookInterestRegistrations` | Get the current webhook interest registration |
| DELETE | `/telephony/webhookInterestRegistrations` | Delete the webhook interest registration |

**Required Scope:** `spark-admin:calls_read`

### Create a Webhook Interest Registration

**POST** `/telephony/webhookInterestRegistrations`

Creates or updates a webhook interest registration. At least one interest is required.

#### Request Body

| **Property** | **Type** | **Required** | **Description** |
|--------------|----------|--------------|-----------------|
| `interests` | array | Yes | Collection of webhook interests. At least one required. Each interest has either `resource` or `actor` set (not both). |
| `duration` | integer | No | Days until expiration. Defaults to 60 days. |

#### Request Example

```json
{
  "interests": [
    { "resource": "Agent" },
    { "actor": "Workspaces" }
  ],
  "duration": 30
}
```

### Get Webhook Interest Registration

**GET** `/telephony/webhookInterestRegistrations`

Returns the current webhook interest registration.

#### Response Example

```json
{
  "interests": [
    { "resource": "Agent" },
    { "actor": "Workspaces" }
  ],
  "expiresAt": "2026-08-01T00:00:00.000Z"
}
```

### Delete Webhook Interest Registration

**DELETE** `/telephony/webhookInterestRegistrations`

Deletes the webhook interest registration.

### Interest Types

#### Resource-based Interests

| **Value** | **Description** |
|-----------|-----------------|
| `Hook Status` | Enables webhook events for the `telephony_hookstatus` resource. |
| `Agent` | Enables webhook events for the `telephony_agent` resource. |
| `Services` | Enables webhook events for the `telephony_services` resource. |
| `Agent Monitoring` | Enables webhook events for the `telephony_agentMonitoring` resource. |
| `Queue` | Enables webhook events for the `telephony_queue` resource. |
| `Queue Monitoring` | Enables webhook events for the `telephony_queueMonitoring` resource. |

#### Actor-based Interests

| **Value** | **Description** |
|-----------|-----------------|
| `Workspaces` | Enables telephony webhook events associated with workspace actors. |
| `Virtual Lines` | Enables telephony webhook events associated with virtual line actors. |

---
