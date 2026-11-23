---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-notifications-screen-pops
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Screen Pop Module
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-notifications-screen-pops). [Full Markdown](../../../../docs/desktop-notifications-screen-pops.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Send Desktop notifications and listen for screen-pop events from custom widgets.

## Selected section

## Screen Pop Module

The `Desktop.screenpop` module makes requests and listens to notification events related to the screen pop entity.

**Example**

```javascript
Desktop.screenpop.addEventListener("eScreenPop", (msg) => logger.info(msg));
```

To remove an event subscription in order to avoid memory leaks, you have the following options:

```javascript
// Module supports removing added listeners like:
const listener = (msg) => logger.info(msg);
Desktop.screenpop.addEventListener("eScreenPop", listener);
Desktop.screenpop.removeEventListener("eScreenPop", listener);

// Module supports one-time added listeners like:
Desktop.screenpop.addOnceEventListener("eScreenPop", listener);
Desktop.screenpop.removeOnceEventListener("eScreenPop", listener);

// Module supports removing all listeners like:
Desktop.screenpop.removeAllEventListeners();
```

### Events

#### eScreenPop

Listens to an event that displays the screen pop.

**Example**

```javascript
Desktop.screenpop.addEventListener("eScreenPop", listener);
```

**Example Response**

```javascript
const eScreenPop = {
  data: {
    agentId: "1736827c-10ef-4b2a-90e0-7d2a3743ded3",
    interactionId: "4745472e-cfa2-47f3-9fc1-16359516d648",
    queryParameters: null,
    screenPopUrl: "https://youtube.com",
    target: "insideDesktop",
    type: "ScreenPop"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_90a4bf42-ba95-47a6-b8cb-c1ed105ff5ea",
  type: "RoutingMessage"
};
```
