---
type: Guide
title: Agent Desktop | Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/desktop
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/desktop)

Extend **Agent Desktop** with custom widgets and the Desktop SDK. Build widgets, manage interactions, and migrate Finesse gadgets for Webex Contact Center.

## Agent Desktop Overview

Desktop combines the flexibility of a cloud service with Cisco security and global scalability. Automating routine tasks helps agents focus on serving customers.

Desktop provides customer interactions—voice, chat, email, and social channels, including Facebook Messenger and SMS—within one unified experience. Custom widgets integrate CRM and other business applications into that experience and reduce application switching.

### Technical Overview

The following diagram shows the relationships between Desktop micro front ends and services.

![Diagram of Desktop architecture](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2de4d09858b194ff/69b1e95e6b116ac8f98e75a5/agentx_architecture_4a33dac1d3.svg)

## Get Started

- [Build Custom Widgets](https://developer.webex.com/docs/desktop-custom-widgets) — choose a widget type, define its properties, and test it inside Desktop.
- [Get Started with the Desktop SDK](https://developer.webex.com/docs/desktop-sdk-getting-started) — install the packages and initialize the SDK.
- [Desktop SDK Reference](https://developer.webex.com/docs/desktop-sdk-reference) — find a module, method, property, or event.

## Widgets and Activities

| Guide | What it covers |
| --- | --- |
| [Build Custom Widgets](https://developer.webex.com/docs/desktop-custom-widgets) | Web Components, iframe widgets, lifecycle updates, inactivity tracking, Momentum UI, and theming. |
| [Widget Data and Desktop Layout](https://developer.webex.com/docs/desktop-widget-data-layout) | STORE fields, layout bindings, and dynamic widget titles. |
| [Popovers](https://developer.webex.com/docs/desktop-popovers) | Anchored panels, composition, positioning, dismissal, and sandbox availability. |

## JavaScript SDK and Modules

### Javascript SDK

The Desktop SDK supports widgets embedded within Desktop. It does not create a separate Desktop. Start with [SDK installation and initialization](https://developer.webex.com/docs/desktop-sdk-getting-started), or use the [complete SDK reference index](https://developer.webex.com/docs/desktop-sdk-reference).

| Reference | What it covers |
| --- | --- |
| [Agent State and Availability](https://developer.webex.com/docs/desktop-agent-state) | Agent information, auxiliary codes, media availability, and granular channel state changes. |
| [Tasks and Call Control](https://developer.webex.com/docs/desktop-call-control) | Tasks, accept/end/wrap-up, hold, recording, and WebRTC call controls. |
| [Consultation and Conferences](https://developer.webex.com/docs/desktop-consultation-conferences) | Consultations, conferences, and participant management. |
| [Transfer Contacts](https://developer.webex.com/docs/desktop-transfers) | Queue, blind, and consult transfers. |
| [Contact Events and Subscriptions](https://developer.webex.com/docs/desktop-contact-events) | Event subscriptions, payloads, widget mounting, and listener cleanup. |
| [Outbound Calls and Scheduled Callbacks](https://developer.webex.com/docs/desktop-outbound-callbacks) | Outbound calls, address books, ANI, CAD updates, and scheduled callbacks. |
| [Notifications and Screen Pops](https://developer.webex.com/docs/desktop-notifications-screen-pops) | Silent, auto-dismiss, and acknowledge notifications, plus screen-pop events. |
| [Keyboard Shortcuts](https://developer.webex.com/docs/desktop-keyboard-shortcuts) | Shortcut registration, modifiers, conflicts, and listeners. |
| [Localization](https://developer.webex.com/docs/desktop-localization) | Localization bundles and lit-element integration. |
| [Logging and Diagnostics](https://developer.webex.com/docs/desktop-logging-diagnostics) | Widget loggers, log downloads, and cleanup. |
| [Supervisor Call Monitoring](https://developer.webex.com/docs/desktop-supervisor-monitoring) | Supervisor monitoring controls, barge-in, and success/failure events. |

## Asynchronous Events

Use [Contact Events and Subscriptions](https://developer.webex.com/docs/desktop-contact-events) to react to interaction changes. For granular availability, use the channel state event documented in [Agent State and Availability](https://developer.webex.com/docs/desktop-agent-state).

## Finesse Gadget Migration

[Migrate Finesse Gadgets](https://developer.webex.com/docs/desktop-finesse-migration) covers embedded applications and JavaScript gadgets, including layout configuration and a Web Component example.
