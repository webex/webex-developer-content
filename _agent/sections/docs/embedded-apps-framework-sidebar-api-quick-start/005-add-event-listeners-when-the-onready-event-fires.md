---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-framework-sidebar-api-quick-start
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Add Event Listeners when the onReady Event Fires
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-framework-sidebar-api-quick-start). [Full Markdown](../../../../docs/embedded-apps-framework-sidebar-api-quick-start.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites and Additional Documentation](001-prerequisites-and-additional-documentation.md)

## Article introduction

The Embedded Apps framework has added the ability to create Sidebar Apps that reside on the left rail of the Webex application.

---

The Embedded Apps framework has added the ability to create Sidebar Apps that reside on the left rail of the Webex application. These Apps can be always ON, i.e. launched when the Webex App is launched. Also, as part of this effort, we have introduced a new set of APIs that lets you add call monitoring and notifications to your embedded apps. You can use the EAF **Sidebar API** to intercept and selectively process incoming call events as well as flexibly manage the status badges that display on your embedded app to indicate notification counts or other actions that need to be addressed by your users such as error states. Status badges are displayed as an overlay on your embedded app icon in the Webex app sidebar:

![Embedded apps in the sidebar with notification counts](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4ed3b73f6fa41dd2/64132852c96f5354275e4268/sidebar-notifications.png)

For incoming calls, the API can return the following call information:

- Call type
- Call state
- Caller information for local and remote participants

You can then use that information to trigger specific business logic for your embedded app. For instance, a medical app could query and display patient profile information, or a Customer Relationship Management (CRM) app could query customer information, displaying current opportunities and contact history. In the screen shot below, a custom (albeit abstracted) App1 screen has been opened for two separate incoming callers:

![Pop up application page keyed from incoming caller details.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt15468ec42c41b20f/6413286fb1f84e5422462e9e/sidebar-popout.png)

In this article we'll build basic application logic to explore some of the features of the new sidebar API.

## Selected section

## Add Event Listeners when the onReady Event Fires

Next, we'll set up two event listeners which are enabled once the application's `onReady` event has fired:

- A listener for sidebar events, `sidebar:callStateChanged`.
- A listener for application view state changes, `application:viewStateChanged`.

### Listen for Call State Changes in the Sidebar

To listen for call state changes in the sidebar, add the following code:

```javascript
embedded_app.onReady().then(() => {
  log("onReady()", { message: "EA is ready." });
  embedded_app.listen().then(() => {
    embedded_app.on("sidebar:callStateChanged", (call) => {
        console.log("Call state changed. New call object:", call);
        handleCallStateChange(call);
    });
  });
});
```

When a call is detected, the `call` object is handed off to a `handleCallStateChange()` function for further processing.

### Listen for View State Changes in the Application

Add another event handler to capture the `application:viewStateChanged` event, `IN_FOCUS`, and decrement the application badge count since this indicates the user has responded to the badge displayed by the `callStateChanged` event by clicking on the embedded app icon:

```javascript
embedded_app.onReady().then(() => {
    log("onReady()", { message: "EA is ready." });
    embedded_app.listen().then(() => {
      embedded_app.on("sidebar:callStateChanged", (call) => {
        console.log("Call state changed. Call object:", call);
        handleCallStateChange(call);
      });
      embedded_app.on("application:viewStateChanged", (viewState) => {
        console.log("View state changed. Current view:", viewState);
        switch (viewState) {
          case "IN_FOCUS":
            // User has noticed the badge and has responded, so we can remove it...
            initializeSideBar(callCount++);
            break;
        }
      });
    });
  });
```
