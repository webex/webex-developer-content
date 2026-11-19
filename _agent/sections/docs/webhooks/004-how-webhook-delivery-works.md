---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhooks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- How webhook delivery works
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webhooks). [Full Markdown](../../../../docs/webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use webhooks to connect Webex activity to your application's workflows, from responding to messages to processing Contact Center events.

## Selected section

## How webhook delivery works

Webhooks send HTTP POST notifications to a destination your application exposes. Register the events you need, store the registration configuration and signing secret, verify each delivery, accept it durably, and process it idempotently. Use the selected family's guide for its acknowledgement rules and recovery behavior.

| Contract | Webex Webhooks API | Contact Center Subscriptions |
| --- | --- | --- |
| Destination field | `targetUrl` | `destinationUrl` |
| Envelope identifier | `id` identifies the webhook registration. It is not an event deduplication key. | `id` identifies a source event. `source` contains the subscription ID. |
| Signature | `X-Spark-Signature`, or `X-Webex-Signature` for supported types | `X-WebexCC-Signature` |
| Version selection | Check the resource's API and event documentation. | Store the Subscription API version and configured resource version; V2 deliveries include timestamp and resource-version headers. |

The Workspace Integration and Webex Connect guides define their own setup, payload, and authentication contracts. Select verification rules from the registration family; a shared HTTP header name alone does not identify the contract.
