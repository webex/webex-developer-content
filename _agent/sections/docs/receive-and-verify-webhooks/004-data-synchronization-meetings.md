---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-webhooks
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Data Synchronization Meetings
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-webhooks). [Full Markdown](../../../../docs/receive-and-verify-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Webhooks API notifications, verify signatures over the original request bytes, and process accepted events without repeating side effects.

## Selected section

## Data Synchronization Meetings

We generally provide webhooks that are actionable. This means the webhook has enough information to be useful to drive most workflow scenarios. We have found some customers who want to query additional details from the REST resource after receiving a webhook. The REST resource may not be immediately in sync with the webhook received, which is sent as soon as possible.
Due to a complex multistage backend, our current SLA is a sync between webhook and REST resource within 10 minutes for 99.5% of cases.
Let’s use a practical example. A developer registers for the meetingParticipants:joined webhook. After the webhook is received the developer wants to query the /meetingParticipants/{id} REST resource. This request may return a 404 as long as the REST resource is synching with the subsystems.
