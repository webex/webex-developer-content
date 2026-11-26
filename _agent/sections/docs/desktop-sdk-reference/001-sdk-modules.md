---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-sdk-reference
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- SDK Modules
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-sdk-reference). [Full Markdown](../../../../docs/desktop-sdk-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Find Desktop SDK modules, methods, properties, and events with links to their detailed reference pages.

## Selected section

## SDK Modules

Initialize the SDK inside Desktop before using a module. See [Get Started with the Desktop SDK](https://developer.webex.com/docs/desktop-sdk-getting-started).

| Module | Purpose | Detailed reference |
| --- | --- | --- |
| `Desktop.config` | Initialize the SDK and register CRM connectors. | [Get Started with the Desktop SDK](https://developer.webex.com/docs/desktop-sdk-getting-started) |
| `Desktop.agentConfigJsApi` | Retrieve paginated idle and wrap-up codes. | [Agent State and Availability](https://developer.webex.com/docs/desktop-agent-state#fetchpaginatedauxcodes) |
| `Desktop.i18n` | Manage localization bundles. | [Localization](https://developer.webex.com/docs/desktop-localization) |
| `Desktop.actions` | Read data, send notifications, add tasks, and control WebRTC calls. | [Tasks and Call Control](https://developer.webex.com/docs/desktop-call-control), [availability](https://developer.webex.com/docs/desktop-agent-state), [notifications](https://developer.webex.com/docs/desktop-notifications-screen-pops), [authentication token](https://developer.webex.com/docs/desktop-sdk-getting-started#gettoken) |
| `Desktop.logger` | Create and collect widget logs. | [Logging and Diagnostics](https://developer.webex.com/docs/desktop-logging-diagnostics) |
| `Desktop.agentStateInfo` | Read agent data and change channel availability. | [Agent State and Availability](https://developer.webex.com/docs/desktop-agent-state), [address books and ANI](https://developer.webex.com/docs/desktop-outbound-callbacks#address-books-and-outbound-ani) |
| `Desktop.agentContact` | Control interactions, consultations, conferences, and transfers. | [Tasks and Call Control](https://developer.webex.com/docs/desktop-call-control), [consultation](https://developer.webex.com/docs/desktop-consultation-conferences), [transfers](https://developer.webex.com/docs/desktop-transfers), [events](https://developer.webex.com/docs/desktop-contact-events) |
| `Desktop.dialer` | Start outbound calls and update CAD variables. | [Outbound Calls and Scheduled Callbacks](https://developer.webex.com/docs/desktop-outbound-callbacks) |
| `Desktop.screenpop` | Listen for screen-pop events. | [Notifications and Screen Pops](https://developer.webex.com/docs/desktop-notifications-screen-pops) |
| `Desktop.shortcutKey` | Register shortcut actions and handle conflicts. | [Keyboard Shortcuts](https://developer.webex.com/docs/desktop-keyboard-shortcuts) |
| `Desktop.monitoring` | Control supervisor call monitoring. | [Supervisor Call Monitoring](https://developer.webex.com/docs/desktop-supervisor-monitoring) |
| `Desktop.webexMetricsInternal` | Track widget behavioral events; documented as an internal module. | [Logging and Diagnostics](https://developer.webex.com/docs/desktop-logging-diagnostics) |
| `Desktop.scheduleCallback` | Manage scheduled callbacks and valid campaign times. | [Outbound Calls and Scheduled Callbacks](https://developer.webex.com/docs/desktop-outbound-callbacks) |
| `Desktop.popover` | Manage anchored popovers in sandboxed widgets. | [Popovers](https://developer.webex.com/docs/desktop-popovers) |
