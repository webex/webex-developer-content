---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-framework-sidebar-api-quick-start
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Example Workflow General Logic
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

## Example Workflow General Logic

For this example, we're going to implement the following basic workflow:

1. With the embedded app pinned to the sidebar in an `ALWAYS_ON` state but also `OUT_OF_FOCUS`, a call comes in and the following event is triggered, `sidebar:callStateChanged`.
2. The app retrieves the `callerID` property for the call object.
3. If the `callerID` value matches to a person of interest in the backing database (simulated here by a hardcoded variable used as the ID for the "VIP").
4. The badge count is on the app is **incremented** to notify the user that an important call has come in, and a message is written to the console that a VIP user has been encountered.
5. The app user notices the the badge on the embedded app and clicks it, triggering the following event, `ON_FOCUS`, in `application:viewStateChanged`, and the badge count is **decremented** because the user has responded to the notification.
6. Back in the call handler, the call data is written to the console, representing persistent call logging.



> **Info**
>
> Even if the caller is not a person of interest, while no badge is displayed, the call itself is logged the same as for the VIP.
