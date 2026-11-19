---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Responsibilities
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel). [Full Markdown](../../../../docs/bring-your-own-custom-messaging-channel.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md) [Authentication For Custom Messaging Integrations](004-authentication-for-custom-messaging-integrations.md) [Attachment URL Requirements](011-attachment-url-requirements.md)

## Article introduction

Connect an external messaging channel to Webex Contact Center through middleware that uses the Custom Messaging APIs.

## Selected section

## Responsibilities

Use this model when your middleware application is responsible for receiving inbound messages from the external messaging channel, forwarding them to Webex Contact Center, and delivering outbound messages from Webex Contact Center back to the end customer.

The middleware application is responsible for:

- Hosting the channel integration
- Obtaining and refreshing OAuth tokens
- Calling the Create Task API for the initial inbound message
- Calling the Task Messages API for subsequent inbound messages
- Processing outbound webhooks received from the asset-level webhook URL
- Subscribing to task lifecycle and inbound message subscription webhooks

Webex Contact Center is responsible for:

- Validating and routing Custom Messaging interactions
- Running the configured flow
- Presenting the conversation to agents
- Generating task lifecycle and task message webhook events
- Storing transcripts for later retrieval
