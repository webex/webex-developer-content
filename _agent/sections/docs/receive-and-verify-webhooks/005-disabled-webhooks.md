---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-webhooks
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Disabled Webhooks
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-webhooks). [Full Markdown](../../../../docs/receive-and-verify-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Webhooks API notifications, verify signatures over the original request bytes, and process accepted events without repeating side effects.

## Selected section

## Disabled Webhooks

Webex can disable a webhook after repeated delivery failures, including an unreachable endpoint or an unsuccessful HTTP response. Failure thresholds and the counting interval are configurable; do not depend on a fixed number of attempts as a retry guarantee. Once disabled, a webhook is not reenabled automatically.

To see the current status of a webhook, use the [Get Webhook Details](https://developer.webex.com/docs/api/v1/webhooks/get-webhook-details) API endpoint. To reactivate a disabled webhook, use the [Update a Webhook](https://developer.webex.com/docs/api/v1/webhooks/update-a-webhook) API endpoint with the `status` parameter set to ‘active’.

Correct the delivery failure before reenabling the webhook. Failure counts can remain until their current counting interval expires, so a reenabled webhook can be disabled again quickly if delivery still fails. Reenabling does not guarantee a fresh failure budget.
