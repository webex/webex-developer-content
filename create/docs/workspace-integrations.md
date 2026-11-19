---
type: Guide
title: Workspace Integrations | Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/workspace-integrations
content_type: documentation
product_group:
- webex-suite
categories:
- app-hub
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/workspace-integrations)

Build **Workspace Integrations** that extend the capabilities of Workspaces and Webex devices through [Webex developer APIs](https://developer.webex.com/docs/getting-started).

## Workspace Integrations Overview

These integrations can be **public** (built by third party vendors that engage with Cisco to provide all customers access to the integration), or they can be **private** (built by and available only to the customers themselves).

![Workspaces](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8bf2173753bd4050/64526bc54bb7677c0819cf9e/poster.jpeg)

For customer Control Hub full administrator users, the integrations framework provides a way to enable a third party vendor to interact with the Webex APIs, and especially the Webex device [xAPI](https://roomos.cisco.com/docs/Introduction.md#the-xapi), in a transparent and controlled manner. It's easy to activate and deactivate integrations, understand what permissions they have been granted, and be in control of changes to these permissions as the integrations evolve.

This article describes how to develop and deploy these integrations, for both third party vendors and customers that want to build private integrations.

## Examples

Here are a couple of examples of what Workspace Integrations can be used for:

* Office map, showing whether meeting rooms are currently occupied or vacant, based on actual people presence from the video device's sensors and AI.
* Controlling the lights and shades in the meeting room from custom UI controls on the device's touch interface.
* Report issues in the meeting room from the touch interface (forward to Service Now or similar service).
* Un-book a booked meeting room when it is detected that nobody showed up.
* Collect feedback on quality of video calls by asking users after the call has ended with a rating dialog.
* Keep track of how much meeting rooms have been used, and when it was last cleaned.

## Requirements

The requirements and skills needed for this integration type is:

* Webex or Webex Edge registered endpoints.
* The knowledge and infrastructure to host a private/internal or public web service that can talk with the Webex APIs, for example a Node.js web server or a Python web server.

## What's the difference between workspaces and devices?

In Webex, **workspaces** typically mean a place where people work, such as an office, a meeting room, a huddle area or a reception. Often, one workspace contains one **collaboration device**, but it can also contain zero or multiple devices.

A device must always belong to one, and only workspace. Note that the device id will change if the device is factory reset, whereas the workspace id will be permanent throughout the lifetime of that space.

A **location** is a physical location that can contain many workspaces. Examples of a typical location is a floor in the building, or an entire building, depending on how the admin would like to logically group the organization.

Workspace integrations can optionally be activated for only selected locations. For example, you can enable catering service integration for only the top floor meeting rooms in a building. The integration will then not have xAPI access to the other devices in that organization.

The following diagram illustrates the topology, where a workspace integration has been enabled for a single location, that contains three workspaces, each with one device.

![Topology](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3e9c38f3c7498467/64526bc5b7de36333cb4ae77/topology.png)

## Comparison with HTTP API Integrations

Workspace Integrations are _not_ the same as the integrations described in [Integrations](https://developer.webex.com/docs/integrations). They have things in common, specifically using the same underlying [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) framework, but differ in a few ways:

1. Workspace integrations are exclusively managed from Control Hub under Workspaces > Integrations.
1. The workspace integration framework was designed to support service to service interaction. The integration runs with the identity of a machine account created in the customer organization, rather than on behalf of a Webex user.
1. Workspace integrations support fine-grained access to the Webex devices xAPI and webhook or message queue change notifications for select xAPI statuses.

## Comparison with on-device integrations (macros)

Unlike [device macros](https://roomos.cisco.com/doc/TechDocs/MacroIntroduction), the integration is external, so the individual devices do not need any provisioning. Support for workspace integrations is built into RoomOS, and as soon as an admin activates the integration in Control Hub, the devices will start sending data that the integration is subscribing too. Similarly, the integration will be able to invoke actions on the video device, such as starting a call or showing a message to the users in the room, without needing to configure access rules for each individual device. Adding a new feature to the integration or fixing a bug simply requires the central integration to be updated, no action is required for each device.

In addition, the granular API control means that each integration can be limited to which APIs and sensor data it can and cannot use. For example, one integration might allow people in a meeting room to order snacks, and thus only require access to user interface extension APIs. Another integration might just require to count the number of people in the room. The admin can then add the third party integrations, safe in the knowledge that they don't have access to more sensitive APIs such as the call history or the meeting calendar.

For a more detailed comparison with other integration types, see the [Integrations Guide on roomos.cisco.com](https://roomos.cisco.com/doc/TechDocs/Integrations).

## Private and public integrations

A workspace integration can be either private or public. Private means that the integration is only available within your organization. An example can be an integration that allows you to order catering to your meeting rooms. You create the custom user interface on the touch panels, and react to user requests by making requests in your organization's internal ordering system. In this case the integration is usually deployed to Control Hub and activated in the same go, by the same person. The integration is developed by people within the organization to solve internal use cases.

A public integration, on the other hand, is available to all Webex customers. An example can be a third party issue reporting system that is available as a paid service. It can be leveraged as workspace integration by the service provider / vendor, by adding user interfaces to the devices and creating issues in the enterprise system when user's report issues. In this case, the vendor creates the app and requests approval from Cisco. If approved, Cisco will deploy the public integration on Control Hub, where it will be available to all Webex customers. Org admins can now discover the integration and activate it without any coding themselves. When activated for an org, the vendor will receive notification and can redirect the customer to their own web page for creating a user, setting up payment details etc. with the vendor.

![Public integrations](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt50834f81842dbe07/64526bc563c7dd1138106487/public-integrations.png)

## Web hooks and long polling

Workspace integrations support notifications, which means that Webex will tell you when a device status changes (for example when a room goes from being empty to detecting a person it it), or when device events occur (such as a user tapping a custom UI extension button.). These can be delivered to you in two different ways: Web hooks or long polling.

Web hooks means that you need to host a public web service, and tell the URL to Control Hub. Webex will then send the notifications to this URL any time an event occurs.

![Web hooks](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt930fe8f0560442e1/64526bc5d54b2910e833f013/how-it-works.png)

Long polling is the "don't call us, we'll call you" approach, meaning that your integration is constantly asking Webex if any new notifications have occurred. Whenever a device reports a notification, Webex will respond to your query. You will then need to ask again for more notifications.

![Long polling](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1544946a45a554fc/64526bc5b4fe3e118d4170d9/workspace-long-polling.png)

The advantage with long polling is that the integration can run on your internal network, and therefore have access to other restricted resources in your building, such as smart building gateways. In addition, it does not require you to host a public web service with HTTPS certification, which can be technically more difficult, or hard due to your company's security policies and restrictions.

It's also easy to develop and test the integration using long polling, since you can run your developer integration straight from your laptop. It's possible to develop using long polling, then run the production app with web hooks. But be aware that you cannot do long polling and web hooks on the same integration at the same time. Webex notifications can only be delivered to a single listener.

## xAPI access rules

In addition to traditional OAuth scopes, Workspace Integrations support fine grained access control for xAPI. This allows admin to inspect and approve with device APIs the integration has access to. This applies to **commands**, **events** and **statuses**. Note that for statuses, the API list both specifies which xStatus you will be able to query, and which you will receive notifications about when it changes.

It is highly recommended to specify each API directly rather than using wild cards. The fewer APIs your integration uses, the less dangerous it feels for an admin to approve it.

Note that for **xConfigurations** there are currently no such granular control, it's all or nothing based on the `spark-admin:devices_read` and`spark-admin:devices_write` scopes.

Note also that for both scopes and xAPI rules, as a developer you can set whether the requested permission is required or not. If not required, the admin may choose to not accept the optional permissions. This is typically for enhancement features that are nice to have but not strictly necessary. If you have optional permissions, you will need to check at runtime whether or not it has been accepted by the admin before using that API.

## The integration manifest

When you create an integration, you must provide a **manifest** to Control Hub to tell what your integration does, and what API scopes and device APIs it needs access to.

You can create the manifest file yourself or use a visual editor available on [GitHub](https://cisco-ce.github.io/workspace-integrations-editor/).

For details, see the technical overview for Workspace Integrations.

![Control Hub Manifest](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltea3a7c98898ec5ee/64526bc5f1b32a119f435022/control-hub-manifest.png)

## Limitations

Workspace Integrations is a powerful and flexible integration type that allows you to do almost anything the devices have to offer. There are a few limitations worth being aware of:

* For **xEvent** and **xStatus** notifications, there is only a small subset of the statuses and events you can subscribe to, such as room analytics, custom UI events, boot events and a few more. For xStatus you will still be able to query all of the public statuses though. See Control Hub > Workspaces for an up-to-date list.
* For devices in personal mode, the integration will not be able to invoke commands that are defined as **privacy impacting**. You can check this for each API on the [roomos.cisco.com API details page](https://roomos.cisco.com/xapi/).
* Even if you limit an integration to a specific location, it will still be able to access configuration for all devices in the organization, if those scopes are set.
* Since all traffic between the devices and the integration go via the Webex cloud, it will be slower than a direct integration such as macros. For most events, including UI events, it should still be ok, but some actions that require direct feedback, such as manual camera control, may not be optimal for this integration type.

## Quick Start

To quickly get started, you can look at the [SDK for Node.js](https://github.com/cisco-ce/workspace-integrations-nodejs). To try it out, you will need:

* A laptop with **Node.js** and **npm** installed
* Some basic Node.js / JavaScript knowledge
* Admin access to Control Hub
* One or more Cisco devices

There is also the [SDK for Java](https://github.com/cisco-ce/workspace-integrations-java). To test it, you will need:

* A laptop with **Java** and preferably **IntelliJ IDEA** installed
* Some basic Java knowledge
* Admin access to Control Hub
* One or more Cisco devices

## Useful links

* [Node.js SDK](https://github.com/cisco-ce/workspace-integrations-nodejs) - Takes care of token handling and low-level HTTP calls for you with a simple, object oriented JavaScript API
* [Java SDK](https://github.com/cisco-ce/workspace-integrations-java) - Takes care of token handling and low-level HTTP calls for you with a simple, object oriented Java API
* [Online manifest editor](https://cisco-ce.github.io/workspace-integrations-editor/) - Visual editor for creating and editing manifests, with completions for scopes and xAPIs
* [xAPI reference docs](https://roomos.cisco.com/xapi) - Browse and search the device's xAPI for commands, status, and configs that your integration will use
* [Webex Device APIs](https://developer.webex.com/docs/device-developers-guide) - Webex APIs you need to use to talk to the device xAPI from your integration
