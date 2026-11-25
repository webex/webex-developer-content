---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-sdk-getting-started
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Javascript SDK
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-sdk-getting-started). [Full Markdown](../../../../docs/desktop-sdk-getting-started.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Install and initialize the Desktop SDK to access Desktop modules from custom widgets.

## Selected section

## Javascript SDK

**Caution:** The JavaScript SDK library can be used to build widgets that are embedded within the Desktop. You cannot use this library outside of the Desktop or to create a new Desktop.

**Note:** The `@wxcc-desktop/sdk-types` library does not support iFrame based widgets.

The Desktop JavaScript SDK is an npm package that allows you to request up-to-date information from the Desktop. Using the SDK, you can request information such as agent details, assigned tasks, details of specific tasks, current browser locale, and the authentication token for Single Sign-On (SSO) integration.

The SDK package allows you to:

- request data to be passed to your widgets through properties and attributes.
- perform more complex operations by consuming and manipulating the system data inside your widget.
- subscribe to data arriving asynchronously.

Some events in the Desktop occur asynchronously. To subscribe to asynchronous events and access data within the payload, you can add a listener. A few examples for asynchronous events are:

- New task offered
- New task assigned
- Consult request created
- Consult ended
- Screen pop arrived

For the complete list of asynchronous events, see [Asynchronous Events](https://developer.webex.com/docs/desktop-contact-events#asynchronous-events).
