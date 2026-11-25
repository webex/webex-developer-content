---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-framework-sidebar-api-quick-start
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Prerequisites and Additional Documentation
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-framework-sidebar-api-quick-start). [Full Markdown](../../../../docs/embedded-apps-framework-sidebar-api-quick-start.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

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
