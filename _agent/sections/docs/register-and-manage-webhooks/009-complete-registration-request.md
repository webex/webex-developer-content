---
type: Excerpt
canonical_url: https://developer.webex.com/docs/register-and-manage-webhooks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Complete registration request
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/register-and-manage-webhooks). [Full Markdown](../../../../docs/register-and-manage-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md) [User Level Scopes for Meeting Related Webhooks](004-user-level-scopes-for-meeting-related-webhooks.md) [Organization/Admin/Compliance Officer Level Scopes for Meeting Related Webhooks](005-organization-admin-compliance-officer-level-scopes-for-meeti.md)

## Article introduction

Register Webex Webhooks API notifications for Messaging, Meetings, Calling, and platform events, then manage registrations owned by your application.

## Selected section

## Complete registration request

Send the following request with your own access token, test space ID, HTTPS destination, and unique signing secret. The placeholders are illustrative; do not send them literally.

```http
POST https://webexapis.com/v1/webhooks
Authorization: Bearer <access-token>
Content-Type: application/json

{
  "name": "Test message created",
  "targetUrl": "https://example.com/webhooks/messages",
  "resource": "messages",
  "event": "created",
  "filter": "roomId=<test-room-id>",
  "secret": "<unique-secret-from-secret-manager>"
}
```
