---
type: Excerpt
canonical_url: https://developer.webex.com/docs/register-and-manage-webhooks
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Receive your first event
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/register-and-manage-webhooks). [Full Markdown](../../../../docs/register-and-manage-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md) [User Level Scopes for Meeting Related Webhooks](004-user-level-scopes-for-meeting-related-webhooks.md) [Organization/Admin/Compliance Officer Level Scopes for Meeting Related Webhooks](005-organization-admin-compliance-officer-level-scopes-for-meeti.md)

## Article introduction

Register Webex Webhooks API notifications for Messaging, Meetings, Calling, and platform events, then manage registrations owned by your application.

## Selected section

## Receive your first event

1. Select a test Webex space your token can access and obtain its room ID with [List Rooms](https://developer.webex.com/docs/api/v1/rooms/list-rooms).
2. Use [Create a Webhook](https://developer.webex.com/docs/api/v1/webhooks/create-a-webhook) with `resource: messages`, `event: created`, `filter: roomId=<test-room-id>`, your HTTPS `targetUrl`, and a unique `secret`. Store the returned registration ID and its secret together. Add the `secret` to the message example above before submitting it.
3. Post a message in that space. Expect a delivery with `resource: messages`, `event: created`, and a `data.id` identifying the message.
4. Verify the delivery signature over its original bytes. Accept the event durably before acknowledging it, then fetch message content with your application token if needed. See [Receive and verify events](https://developer.webex.com/docs/receive-and-verify-webhooks).
5. Inspect the registration with [Get Webhook Details](https://developer.webex.com/docs/api/v1/webhooks/get-webhook-details). The envelope `id` should match this registration, not the individual message.
6. Delete only this test registration with [Delete a Webhook](https://developer.webex.com/docs/api/v1/webhooks/delete-a-webhook).

<a id="webex-webhooks"></a>
