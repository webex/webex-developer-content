---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-framework-sidebar-api-quick-start
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Handle the Call State
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

## Handle the Call State

With the event handlers in place, we'll now create a function to handle call state changes:

```javascript
function handleCallStateChange(call) {
  switch (call.state) {
    case "Started":
      console.log("A call has come in...");
      
      // Check to see if the call is from a VIP...
      if (call.id === importantContactId) {
        console.log("A VIP call is incoming! Notify the user...");
        // Initialize the sidebar, passing in the incremented the badge count...
        initializeSideBar(callCount++);
      }
      
      // For all calls, log the information...
      console.log("*** CALL INFORMATION ***")
      console.log("- Caller ID: ", call.id);
      console.log("- Call type: ", call.callType);
      console.log("- Call state: ", call.state);
      console.log("- Local Participant: ", call.localParticipant);
      console.log("- Remote Participants list: ", call.remoteParticpants);
      break;
    case "Connected":
      console.log("Call is connected.");
      break;
    case "Ended":
      console.log("Call is ended.");
      break;
    default:
      break;
  }
}
```

The function checks the `state` property of the `call` object passed to it. If the call is in the state `Started`, it checks to see if `call.id` matches the value set for `importantContactId`. If there's a match, then the user is notified via the `initializeSideBar` function which takes an incremented `callCount` as its argument. Note that the `importantContactId` check in an actual production app represents a call to your own app's backend data source. We're just using the hard-coded value here by way of example.

For all incoming calls, whether VIP or not, `call` object metadata is logged to the console. It's up to you whether you'd want only contacts of interest logged or all contacts.

A couple of other call states are intercepted here as well, `Connected` and `Ended`. Again, you may find processing these call events useful in your own app.
