---
type: Guide
title: Embedded Apps Framework Sidebar API Quick Start
display_title: Sidebar API Quick Start
canonical_url: https://developer.webex.com/docs/embedded-apps-framework-sidebar-api-quick-start
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/embedded-apps-framework-sidebar-api-quick-start)

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

## Prerequisites and Additional Documentation

Before continuing, this article assumes you are completely familiar with Webex Embedded App development as described in the [Embedded App Developer Guide](https://developer.webex.com/docs/embedded-apps-guide). We'll only be going over specifics related to the new call monitoring/notification functionality and won't cover any implementation steps required for a fully functional embedded app.

### Changes from EAF Version 1.x to 2.x

There have been a variety of significant changes to the 2.x EAF SDK which will require that you update your existing embedded app:

#### The User API and Events have been deprecated

- The `user` object is static, and, therefore, the `context.getUser()` method is deprecated.
- There are no real-time updates for the `user` object, so the event `user:infoChanged` is also deprecated.

#### The Webex Internal Object has been Removed

The `webex` object has been made private and removed from the global namespace.

#### The webex.application Object has been Changed

The `webex.Application` that used to be an instance of the `Webex.Application` class has been replaced with `webex.Application` as the class itself, meaning that whatever was accessed as part of `webex.Application` is now part of its object instead.

In the 1.x EAF API, calls such as...

```javascript
const about = webex.Application.about;
const capabilities = webex.Application.capabilities;
const deviceType = webex.Application.deviceType;
```

... are now defined in the 2.x EAF API in the following manner:

```javascript
const app = new webex.Application();
const about = app.about;
const capabilities = app.capabilities;
const deviceType = app.deviceType;
```

For a complete list of properties, accessors and methods, see the details on the [Application class](https://eaf-sdk.webex.com/classes/Application.html).

#### Log levels

The Embedded App SDK 2.x allows the user to set and modify the log level at Application instance creation or at a later time. Default log level is set to INFO.

**While creating application instance**

```javascript
const config = {
  logs: {
    logLevel: 0   //INFO: 0, WARN: 1, ERROR: 2, SILENT: 3
  }
}
const app = new window.Webex.Application(config);  //CDN
OR
const app = new Application(config);  //NPM
```

**Using log property on application instance**

```javascript
app.log.updateLogLevel(0);  //INFO: 0, WARN: 1, ERROR: 2, SILENT: 3
```

### API Documentation

You can find the latest documentation for the new sidebar API here:

- <https://eaf-sdk.webex.com/interfaces/IWebexAppsSidebar.html>

For the complete API reference, see:

- <https://eaf-sdk.webex.com/index.html>

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



## Include the 2.0 EAF SDK in your Application

To include the EAF SDK in your application add the following `<script>` tag in your `<head>` element:

```html
<head>
    ...
    <script src="https://unpkg.com/@webex/embedded-app-sdk@latest" defer />
    ...
</head>
```

## Initialize Some Basic State

We'll need a few global objects for our call processing app:

```javascript
var embedded_app = new window.webex.Application();
var sidebar;
var callCount;
var importantContactId = "(214) 555-1212";
```

We've got the main embedded app application object instance as well as a variable to hold the sidebar instance and a call counter variable to track incoming calls. The `importantContact` variable is just something set to imitate a VIP caller coming in that you'd want to be notified about.

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

## Where to Go Next

We've covered the basic workflow for handling sidebar events and notifications, but you can try the [Embedded Apps Kitchen Sink](https://eaf-sdk.webex.com/samples/) to explore all of the features of EAF 2.x, including notifications. The kitchen sink includes a variety of utility functions you may find useful in your own embedded app, including:

- Multiple state storage options including cookies, localStorage, and sessionStorage.
- A logging function that lets you append log details to an HTML control for debugging convenience.
- Additional examples for call monitoring including querying calls and setting badge options.

## Getting Support

For support on EAF 2.0, please visit our [Support Page](https://developer.webex.com/support).
