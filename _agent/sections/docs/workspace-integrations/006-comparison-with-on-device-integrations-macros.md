---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspace-integrations
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Comparison with on-device integrations (macros)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/workspace-integrations). [Full Markdown](../../../../docs/workspace-integrations.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements](003-requirements.md) [Limitations](011-limitations.md)

## Article introduction

Build **Workspace Integrations** that extend the capabilities of Workspaces and Webex devices through [Webex developer APIs](https://developer.webex.com/docs/getting-started).

## Selected section

## Comparison with on-device integrations (macros)

Unlike [device macros](https://roomos.cisco.com/doc/TechDocs/MacroIntroduction), the integration is external, so the individual devices do not need any provisioning. Support for workspace integrations is built into RoomOS, and as soon as an admin activates the integration in Control Hub, the devices will start sending data that the integration is subscribing too. Similarly, the integration will be able to invoke actions on the video device, such as starting a call or showing a message to the users in the room, without needing to configure access rules for each individual device. Adding a new feature to the integration or fixing a bug simply requires the central integration to be updated, no action is required for each device.

In addition, the granular API control means that each integration can be limited to which APIs and sensor data it can and cannot use. For example, one integration might allow people in a meeting room to order snacks, and thus only require access to user interface extension APIs. Another integration might just require to count the number of people in the room. The admin can then add the third party integrations, safe in the knowledge that they don't have access to more sensitive APIs such as the call history or the meeting calendar.

For a more detailed comparison with other integration types, see the [Integrations Guide on roomos.cisco.com](https://roomos.cisco.com/doc/TechDocs/Integrations).
