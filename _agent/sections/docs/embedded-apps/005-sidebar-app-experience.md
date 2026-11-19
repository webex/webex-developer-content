---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Sidebar App Experience
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps). [Full Markdown](../../../../docs/embedded-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex Embedded Apps Framework allows Webex users to seamlessly interact with your third party application from within Webex.

---

The Webex Embedded Apps Framework lets you easily integrate your existing web applications into Webex meetings and spaces. Webex Embedded Apps present a seamless user experience, and, as with Webex itself, can run across multiple platforms, including Windows, Mac, Linux, iOS and Android.

This guide provides the following:

- Overview of the [embedded app experience](https://developer.webex.com/docs/embedded-apps#about-embedded-apps-in-spaces-and-meetings) in Meetings and Spaces
- [Developer quick start](https://developer.webex.com/docs/embedded-apps-guide#developer-quick-start)
- [Embedded Apps Framework API Reference](https://developer.webex.com/docs/embedded-apps-api-reference)
-  [Design guidelines and considerations](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings) for apps running in [meeting](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings), [messaging](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces) and [device](https://developer.webex.com/docs/embedded-apps-for-webex-devices) contexts.

[Create an Embedded App](<https://developer.webex.com/my-apps/new/embedded-app>)



> **Success**
>
> As of Webex app version 44.3, we’ve integrated the Webex AppHub natively into the Webex app itself, allowing your users to explore Apphub to discover apps and bots without the need to leave the Webex application! For more information, see [What's New](https://developer.webex.com/docs/embedded-apps-whats-new).





> **Info**
>
> Webex for Government (FedRAMP) customers are limited to creating private Embedded Apps and cannot submit Embedded Apps to Webex App Hub.





> **Info**
>
> If you are not currently a Webex customer you can [request a developer sandbox](https://developer.webex.com/docs/developer-sandbox-guide) to start developing embedded apps. Free Webex user accounts cannot be used to create embedded apps.

## Selected section

## Sidebar App Experience



> **Warning**
>
> Not supported for Webex for Government (FedRAMP)



Sometimes, you’ll want to have your embedded app available **outside** of explicit meetings and spaces. As an example, let's look at a CRM application. An end user sales agent wants to run an app that loads the CRM profile of a caller **before** answering a call so that they are prepared to edit the caller's profile or gather essential information to help with closing a deal. The embedded app developer can configure the embedded as **always ON** when building the app, meaning that the app launches and is always running in the background when the Webex app launches, and is always able to listen to incoming call events.

When a call comes in, the app can detect the call, extract the caller's number, and use that number to load the corresponding CRM profile:

```javascript
app.on("sidebar:callStateChanged", (call) => {
    if (call.state = "Started") { 
        const calling_number = call.id; 
    } 
}); 
```

In order grab the sales agent's attention, the app can show a notification badge, prompting the agent to click on the embedded app:

```javascript
const badge = { 
  badgeType: 'count', 
  count: 1, 
}; 
const sidebar = await app.getSidebar();
sidebar.showBadge(badge); 
```

![incremented badge](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5d39e7f208147ec7/642ed8e2200d4610808220a3/sidebar-app-message.png)

Once the agent clicks on the app, the loaded profile is shown, and the app is notified that it’s now in focus:

```javascript
app.on("application:viewStateChanged", (viewState) => {
  if (viewState == "IN_FOCUS") {
    // Display the CRM record...
}
```

The app then displays the CRM record for the caller:

![loaded CRM profile for App1](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd9bdc06adffc2c3f/642ed8e25f168f10bc19f737/sidebar-app-1-select.png)

### Sidebar Notes

- Sidebar apps are available in the Webex client but not in the Meeting Center client. Also, sidebar apps are not supported on Mobile and Cisco devices at the moment.
- Each organization has a limit of **3** always ON sidebar apps.
