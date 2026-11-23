---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspace-integrations
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Private and public integrations
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/workspace-integrations). [Full Markdown](../../../../docs/workspace-integrations.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements](003-requirements.md) [Limitations](011-limitations.md)

## Article introduction

Build **Workspace Integrations** that extend the capabilities of Workspaces and Webex devices through [Webex developer APIs](https://developer.webex.com/docs/getting-started).

## Selected section

## Private and public integrations

A workspace integration can be either private or public. Private means that the integration is only available within your organization. An example can be an integration that allows you to order catering to your meeting rooms. You create the custom user interface on the touch panels, and react to user requests by making requests in your organization's internal ordering system. In this case the integration is usually deployed to Control Hub and activated in the same go, by the same person. The integration is developed by people within the organization to solve internal use cases.

A public integration, on the other hand, is available to all Webex customers. An example can be a third party issue reporting system that is available as a paid service. It can be leveraged as workspace integration by the service provider / vendor, by adding user interfaces to the devices and creating issues in the enterprise system when user's report issues. In this case, the vendor creates the app and requests approval from Cisco. If approved, Cisco will deploy the public integration on Control Hub, where it will be available to all Webex customers. Org admins can now discover the integration and activate it without any coding themselves. When activated for an org, the vendor will receive notification and can redirect the customer to their own web page for creating a user, setting up payment details etc. with the vendor.

![Public integrations](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt50834f81842dbe07/64526bc563c7dd1138106487/public-integrations.png)
