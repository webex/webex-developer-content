---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-framework-sidebar-api-quick-start
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Displaying Notifications
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

## Displaying Notifications

You can send notifications from your sidebar app that appear in Webex and in the system dock or notification center. Use the sidebar's `showNotification(message, redirectURL)` method, documented in [IWebexAppsSidebar#showNotification](https://eaf-sdk.webex.com/interfaces/IWebexAppsSidebar.html#showNotification).

After obtaining the sidebar instance via `context.getSidebar()` (for example, in the same way you do for badges), call `showNotification` with a message string and a URL to open when the user clicks the notification:

```javascript
embedded_app.context.getSidebar().then((sidebar) => {
  sidebar.showNotification("You have a new message", "https://example.com/messages/123")
    .then((success) => {
      console.log("Notification shown:", success);
    })
    .catch((error) => {
      console.log("showNotification failed. Error: ", Webex.Application.ErrorCodes[error]);
    });
});
```

### How to test notifications

1. Follow this quick start to run an embedded sidebar app, or open the [Embedded Apps Kitchen Sink](https://eaf-sdk.webex.com/samples/) and use the Sidebar section.
2. Ensure your app is loaded in the Webex sidebar and has sidebar context (e.g. `getSidebar()` resolves).
3. Trigger `showNotification("Your message", "https://example.com")` from a button click or other event in your app.
4. Confirm the notification appears in Webex and, where supported, in the system dock or OS notifications.
5. Click the notification and verify it opens the redirect URL.
