---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Subscribe Before Sending Traffic
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel). [Full Markdown](../../../../docs/bring-your-own-custom-messaging-channel.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md) [Authentication For Custom Messaging Integrations](004-authentication-for-custom-messaging-integrations.md) [Attachment URL Requirements](011-attachment-url-requirements.md)

## Article introduction

Connect an external messaging channel to Webex Contact Center through middleware that uses the Custom Messaging APIs.

## Selected section

## Subscribe Before Sending Traffic

Before using the Create Task API and the Task Messages API, configure subscription webhooks for the task and task-message events that your middleware application needs to process.

At a minimum, subscribe to:

- `task:failed`
- `task-message:appended`
- `task-message:append-failed`

It is also recommended to subscribe to `task:new` and any other task lifecycle events your implementation needs.

Use the [Subscriptions API](https://developer.webex.com/webex-contact-center/docs/api/v1/subscriptions) to register the subscription, and refer to the [Webhooks guide](https://developer.webex.com/docs/webhooks-cc) for payload details and correlation behavior.
