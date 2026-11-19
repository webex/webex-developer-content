---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Error Handling And Recovery
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel). [Full Markdown](../../../../docs/bring-your-own-custom-messaging-channel.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md) [Authentication For Custom Messaging Integrations](004-authentication-for-custom-messaging-integrations.md) [Attachment URL Requirements](011-attachment-url-requirements.md)

## Article introduction

Connect an external messaging channel to Webex Contact Center through middleware that uses the Custom Messaging APIs.

## Selected section

## Error Handling And Recovery

The middleware application should treat `task:failed` and `task-message:append-failed` as the main failure events for create-task and inbound append operations.

Important guidance:

- `task:failed` is the failure event for create-task failures
- `task-message:append-failed` is the failure event for inbound task-message failures
- Representative append-failure reasons include `INVALID_CONTENT`, `INTERNAL_ERROR`, and `NOT_FOUND`

For stuck-contact recovery:

- If the middleware application receives `task:failed` for a `CONVERSATION_ALREADY_OPEN` condition
- Take the earlier task identifier from the error message
- Call [End Task](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/end-task) only when you have confirmed that the earlier task should be closed.
- Be cautious before ending the earlier task, because it may still be in a valid queued or active state. Only use End Task when you have confirmed that the earlier task is stale and should be closed
- Retry Create Task only after the existing task has been cleaned up, if your workflow requires a retry
