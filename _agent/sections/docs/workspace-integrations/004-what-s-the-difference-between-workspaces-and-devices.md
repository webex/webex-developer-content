---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspace-integrations
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- What's the difference between workspaces and devices?
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/workspace-integrations). [Full Markdown](../../../../docs/workspace-integrations.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements](003-requirements.md) [Limitations](011-limitations.md)

## Article introduction

Build **Workspace Integrations** that extend the capabilities of Workspaces and Webex devices through [Webex developer APIs](https://developer.webex.com/docs/getting-started).

## Selected section

## What's the difference between workspaces and devices?

In Webex, **workspaces** typically mean a place where people work, such as an office, a meeting room, a huddle area or a reception. Often, one workspace contains one **collaboration device**, but it can also contain zero or multiple devices.

A device must always belong to one, and only workspace. Note that the device id will change if the device is factory reset, whereas the workspace id will be permanent throughout the lifetime of that space.

A **location** is a physical location that can contain many workspaces. Examples of a typical location is a floor in the building, or an entire building, depending on how the admin would like to logically group the organization.

Workspace integrations can optionally be activated for only selected locations. For example, you can enable catering service integration for only the top floor meeting rooms in a building. The integration will then not have xAPI access to the other devices in that organization.

The following diagram illustrates the topology, where a workspace integration has been enabled for a single location, that contains three workspaces, each with one device.

![Topology](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3e9c38f3c7498467/64526bc5b7de36333cb4ae77/topology.png)
