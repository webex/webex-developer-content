---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Common Payload Fields
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## Common Payload Fields

The following fields appear across many notification payloads and keep the same general meaning wherever they are used.

| **Field**         | **Description**                                                                                                |
|-------------------|----------------------------------------------------------------------------------------------------------------|
| `eventType`       | Top-level category of the notification payload.                                                                |
| `type`            | Specific notification event name for the payload.                                                              |
| `orgId`           | Unique identifier of the organization associated with the event.                                               |
| `agentId`         | Unique identifier of the agent associated with the event, when applicable.                                     |
| `interactionId`   | Unique identifier of the interaction associated with the event, when applicable.                               |
| `interaction`     | Interaction details associated with the event. Refer to [Interaction](https://developer.webex.com/docs/contact-control-apis#interaction). |
| `queueMgr`        | Queue manager associated with the event, when applicable.                                                      |
| `mediaResourceId` | Identifier of the media resource associated with the event, when applicable.                                   |
| `trackingId`      | Unique identifier used to trace the request or event flow across systems.                                      |
| `eventTime`       | Time at which the event occurred, in epoch milliseconds.                                                       |
| `agentSessionId`  | Unique identifier of the active agent session associated with the event, when applicable.                      |
| `queueId`         | Unique identifier of the queue associated with the event, when applicable.                                     |
