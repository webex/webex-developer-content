---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Before You Begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel). [Full Markdown](../../../../docs/bring-your-own-custom-messaging-channel.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication For Custom Messaging Integrations](004-authentication-for-custom-messaging-integrations.md) [Attachment URL Requirements](011-attachment-url-requirements.md)

## Article introduction

Connect an external messaging channel to Webex Contact Center through middleware that uses the Custom Messaging APIs.

## Selected section

## Before You Begin

Before integrating, ensure that the administrator has configured the following in Control Hub:

- A `Custom Messaging` channel with:
  - Messaging policies for text and attachments
- A `Custom Messaging` asset with:
  - Business address
  - Webhook URL
  - Webhook secret
- A `Custom Messaging` entry point mapped to a `Custom Messaging` flow
- Other Contact Center routing objects required for the interaction, such as queues, teams, and multimedia profiles
