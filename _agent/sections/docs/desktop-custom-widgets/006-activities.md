---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-custom-widgets
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Activities
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-custom-widgets). [Full Markdown](../../../../docs/desktop-custom-widgets.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Build and test Web Components and iframe widgets for Webex Contact Center Desktop.

## Selected section

## Activities

### IdleInActivityTracker

The `idleInActivityTracker` method tracks every interaction of a user with the Desktop. The
administrator configures the Desktop inactivity timeout value. If the agent is inactive on the Desktop for a specified duration, the agent is notified with the <b>Prolonged Inactivity</b> dialog box. The dialog
box is displayed one minute before the configured timeout occurs, and the agent must take action before the
timer runs out.
The `iFrame` windows are isolated from the parent window. To track any user events inside a widget that is
rendered within an iFrame, use the `postMessage()` method.
To handle inactivity timer inside an iFrame:

1. Ensure that your widget or application is running inside an iFrame.
2. Register an event listener for the eventTypes `click`, `wheel`, and `keydown`.
3. Use the `postMessage()` method to communicate the eventTypes to the Desktop (parent window) on
   `wxcc-desktop-iframe-widget-event`.

Add the following code to the main JavaScript file of an iframe widget. Replace `desktopOrigin` with the exact origin of the parent Desktop deployment:

```javascript
// Use the exact HTTPS origin of your Desktop deployment.
const desktopOrigin = "https://desktop.wxcc-us1.cisco.com";
const eventTypes = ["click", "wheel", "keydown"];

function reportActivity(userEvent) {
  window.parent.postMessage({
    key: "wxcc-desktop-iframe-widget-event",
    type: userEvent.type
  }, desktopOrigin);
}

if (window.self !== window.top) {
  for (const eventType of eventTypes) {
    window.addEventListener(eventType, reportActivity);
  }
}

// Call this when the widget is disposed.
function cleanupActivityTracker() {
  for (const eventType of eventTypes) {
    window.removeEventListener(eventType, reportActivity);
  }
}
```
