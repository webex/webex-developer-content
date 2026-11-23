---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel). [Full Markdown](../../../../docs/bring-your-own-custom-messaging-channel.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md) [Authentication For Custom Messaging Integrations](004-authentication-for-custom-messaging-integrations.md) [Attachment URL Requirements](011-attachment-url-requirements.md)

## Article introduction

Connect an external messaging channel to Webex Contact Center through middleware that uses the Custom Messaging APIs.

## Selected section

## Overview

New

**This feature is currently in Beta. Contact your Cisco team if you want access to this feature.**

In this model:

- A middleware application owns the external messaging channel integration.
- Webex Contact Center owns the contact-center task lifecycle.
- Administrators configure the messaging channel, asset, webhook target, entry point, and flow.
- The middleware application uses public APIs to create tasks and append inbound messages, receives outbound messages through the configured webhook, subscribes to task lifecycle events, and retrieves transcripts.
