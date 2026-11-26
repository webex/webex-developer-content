---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-framework-sidebar-api-quick-start
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Notify the User about the VIP Call
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

## Notify the User about the VIP Call

When the VIP `call.id` is detected, we'll then initialize the sidebar and display a badge on our embedded app. In the following screenshot, badges are shown for two embedded apps in the sidebar, App1 and App2:

![The app sidebar.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt150ed54574d46c83/6413283d957f0f55ef8e97b8/sidebar-focus.png)

### Initialize the Sidebar and Display the Badge

The app context `getSidebar()` method returns an instance of the Webex sidebar which is then passed to the `handleBadge()` function along with the `callCount` variable which was incremented while being passed in`handleCallStateChange()`:

```javascript
function initializeSideBar(callCount) {
  embedded_app.context.getSidebar().then((s) => {
      sidebar = s;
      console.log("Show a badge on the sidebar...")
      handleBadge(callCount, sidebar);
    })
    .catch((error) => {
      console.log("getSidebar() failed. Error: ", Webex.Application.ErrorCodes[error]);
    });
}
```

The `handleBadge()` function checks that the sidebar is initialized and then creates a new badge object using the `callCount` variable. The sidebar's `showBadge()` method is used to display the actual badge on the embedded app icon:

```javascript
function handleBadge(callCount, sidebar) {
  // Make sure the sidebar is available..
  if (!sidebar) {
    console.log("Sidebar info is not available. Error: ", Webex.Application.ErrorCodes[4]);
    return;
  }

  // Initialize a badge object...
  const badge = {
    badgeType: 'count',
    count: callCount,
  };

  // Show the badge...
  sidebar.showBadge(badge).then((success) => {
      console.log("sidebar.showBadge() successful.", success);
    }).catch((error) => {
      console.log("sidebar.showBadge() failed. Error: ", Webex.Application.ErrorCodes[error]);
    });
}
```
