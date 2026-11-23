---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspace-integrations
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Web hooks and long polling
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/workspace-integrations). [Full Markdown](../../../../docs/workspace-integrations.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements](003-requirements.md) [Limitations](011-limitations.md)

## Article introduction

Build **Workspace Integrations** that extend the capabilities of Workspaces and Webex devices through [Webex developer APIs](https://developer.webex.com/docs/getting-started).

## Selected section

## Web hooks and long polling

Workspace integrations support notifications, which means that Webex will tell you when a device status changes (for example when a room goes from being empty to detecting a person it it), or when device events occur (such as a user tapping a custom UI extension button.). These can be delivered to you in two different ways: Web hooks or long polling.

Web hooks means that you need to host a public web service, and tell the URL to Control Hub. Webex will then send the notifications to this URL any time an event occurs.

![Web hooks](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt930fe8f0560442e1/64526bc5d54b2910e833f013/how-it-works.png)

Long polling is the "don't call us, we'll call you" approach, meaning that your integration is constantly asking Webex if any new notifications have occurred. Whenever a device reports a notification, Webex will respond to your query. You will then need to ask again for more notifications.

![Long polling](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1544946a45a554fc/64526bc5b4fe3e118d4170d9/workspace-long-polling.png)

The advantage with long polling is that the integration can run on your internal network, and therefore have access to other restricted resources in your building, such as smart building gateways. In addition, it does not require you to host a public web service with HTTPS certification, which can be technically more difficult, or hard due to your company's security policies and restrictions.

It's also easy to develop and test the integration using long polling, since you can run your developer integration straight from your laptop. It's possible to develop using long polling, then run the production app with web hooks. But be aware that you cannot do long polling and web hooks on the same integration at the same time. Webex notifications can only be delivered to a single listener.
