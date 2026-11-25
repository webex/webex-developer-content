---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspace-integrations
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Limitations
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/workspace-integrations). [Full Markdown](../../../../docs/workspace-integrations.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements](003-requirements.md)

## Article introduction

Build **Workspace Integrations** that extend the capabilities of Workspaces and Webex devices through [Webex developer APIs](https://developer.webex.com/docs/getting-started).

## Selected section

## Limitations

Workspace Integrations is a powerful and flexible integration type that allows you to do almost anything the devices have to offer. There are a few limitations worth being aware of:

* For **xEvent** and **xStatus** notifications, there is only a small subset of the statuses and events you can subscribe to, such as room analytics, custom UI events, boot events and a few more. For xStatus you will still be able to query all of the public statuses though. See Control Hub > Workspaces for an up-to-date list.
* For devices in personal mode, the integration will not be able to invoke commands that are defined as **privacy impacting**. You can check this for each API on the [roomos.cisco.com API details page](https://roomos.cisco.com/xapi/).
* Even if you limit an integration to a specific location, it will still be able to access configuration for all devices in the organization, if those scopes are set.
* Since all traffic between the devices and the integration go via the Webex cloud, it will be slower than a direct integration such as macros. For most events, including UI events, it should still be ok, but some actions that require direct feedback, such as manual camera control, may not be optimal for this integration type.
