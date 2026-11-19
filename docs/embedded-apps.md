---
type: Guide
title: Embedded Apps Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/embedded-apps
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/embedded-apps)

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



## Why Embedded Apps?

Webex users collaborate with each other both in real-time during Webex meetings and on an ongoing basis in Webex spaces. However, the information that they need to reference often resides in other web-based applications, requiring them to switch contexts and their focus between the meeting or in-space discussion and the external application. Webex Embedded Apps facilitate surfacing those other applications **directly within the Webex in-meeting and in-space interfaces**, making it frictionless for users to reference specific 3rd party application content and enabling other participants to access and interact with it directly:

![Webex embedded app collaboration](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf9ed1312243f077d/61776434c84e4d1bb61ddb33/ea-meetings-static-hero.png)

## About Embedded Apps in Spaces and Meetings

This section provides a high-level overview of the user experience for using embedded apps in Webex meetings and spaces. In each case the process starts with a meeting participant clicking the **Apps** button (in a meeting) or tab (in a space) to view the list of available apps, and then opening your app.

![Buttons to open list of embedded apps in meeting and spaces](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc3e0083aadb688f5/617764eab685fa1bb581b759/app-btns.png)

The app the user opens is called the _initiator app_ and is the one specified by your app's "Start Page URL" when you [create a new embedded app in the Developer Portal](https://developer.webex.com/docs/embedded-apps-guide#creating-your-embedded-app). The purpose of the initiator app is to share the URL of an app &mdash; the _shared app_ &mdash; that is either [opened with meeting participants](https://developer.webex.com/docs/embedded-apps#inmeeting-app-experience) in real-time, or [added as a tab to a space](https://developer.webex.com/docs/embedded-apps#inspace-app-experience).


This URL is passed the framework's [setShareUrl()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+setShareUrl) method, which causes an **Open for all** or **Add to tab** button to appear in the initiator app's window, depending if the app is running in a meeting or space, respectively. Read more the user experience of [in-meeting](https://developer.webex.com/docs/embedded-apps#inmeeting-app-experience) and [in-space](https://developer.webex.com/docs/embedded-apps#inspace-app-experience) embedded apps.

## In-Meeting App Experience - Interactive experience

For purposes of discussion we'll look at an app for an online polling service. The initiator app in this example (shown below) lets the user create poll questions that are shared with meeting participants. Participants can select an option and send their answer. The initiator app also provides a view for observing live poll results.

![Initiator app being configured to share poll](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt0a9dc1541b89aab6/61776548ac68a827432693ac/meeting-create-poll.png)

When the user is ready to share the poll they click **Create poll**, which invokes the `setShareUrl()` method, passing it the unique URL for the poll and a string for the window title. The initiator app obtains the poll URL from a custom polling service and passes it to `setShareUrl()`:

```javascript
function createPoll() {
    // Custom app code to get poll instance for given configuration
    var pollURL = pollService.getPollUrl(pollConfig);
    app.setShareUrl(pollUrl, "", "Proposal Poll");
}
```

Calling `setShareUrl()` also causes the **Open for all** button to appear in the initiator app's window.

![Open for all button in meeting](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc33b778c35897d84/62aa5f424a98d755621a45f8/meeting-open-together.png)

Clicking this button opens the shared URL in a sidebar window for all meeting participants, as shown below. Participants can also click a button in the window's title bar to open it in a separate window. In this case the app lets participants select a poll option and submit their answer.

![Meeting participant viewing poll](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9efd0d9e5d6cd271/617765fc99dfaf274905ca5e/meeting-participant-view.png)

In the initiator app the user can view poll results as they are tabulated. To end the sharing session &mdash; that is, close the app window for all meeting participants &mdash; the user of the initiator app clicks **Close for all**, which has replaced the **Open for all** button.

![Initiator app viewing  poll results](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf8deab72e932f346/62aa6acae75cbf5ab676a28d/meeting-open-together-results.png)

The initiator app calls [clearShareUrl()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+clearShareUrl) to hide the **Open for all** button.

```javascript
app.clearShareUrl();
```

Notes:

* The meeting host or co-host(s) will see the **Close for all** button when a sharing session is in progress, even if they did not click **Open for all** to start the session. This provides hosts with the ability to end a sharing sessions even if they didn't start it themselves.
* For a given meeting, only one sharing session can be started at a time. If a meeting participant starts a sharing session via one initiator app, and then tries to start another session with a different initiator app, the participant is prompted if they would like to stop the current session and start a new one.

    ![Dialog to swap sharing sessions](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt76ad2816f5cf0e2a/6170987cfa86b41ef7467688/new-app-new-session.png)

    If a meeting participant starts a sharing session and a second user tries to start another session, the second user will see the following error dialog.

    ![Sharing session already in progress error](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9a5711c8def3feb5/61709568a52d96289195bfda/app-in-session-error.png)

    Apps can avoid the latter scenario by checking if a [sharing session is in progress](https://developer.webex.com/docs/embedded-apps-guide#check-for-existing-session) before calling `setShareUrl()`.
    
    
### In-Meeting App Experience - Screen Share Your App!

In some use cases as education, sales pitches, etc, the interactive experience is not desired and the app's initiator would like to just screen share his app to all meeting's participants. This will provide a screen share (read-only) of the app. For purposes of discussion we'll look at an app for content sharing service. The initiator app in this example (shown below) lets the user present certain content from the app to all meeting participants.

![Content sharing embedded app](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5332e3b09aa03012/642445cb524c8410f07bd888/8.png)

When the user is ready to share, they click on the desired content, which invokes the `setPresentationUrl()` method, passing it the unique URL for the content to be shared, title for the shared content, optimization mode which optimize the share content for video/motion, text/images or auto detect and finally if audio should be shared as well or not. The initiator app obtains the content URL from a content service and passes it to `setPresentationUrl()`:

```javascript
function shareContent() {
    // Custom app code to get shared content's URL and share it in meeting
    var contentURL = contentService.getcontentUrl(contentConfig);
    meeting.setPresentationUrl(contentUrl, "My presentation", Webex.Application.ShareOptimizationMode.AUTO_DETECT, false);
}
```

Calling `setPresentationUrl()` also causes the **Share this app content** button to appear in the initiator app's window.

![Share this app content button in meeting](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltca5bdc3744c19124/642445cbde06a31192f4358c/7.png)

Clicking this button shares the content URL in the stage view for all meeting participants, as shown below. To end the sharing session &mdash; that is, stop screen sharing the app's window to all the meeting participants &mdash; the user of the initiator app clicks the **Stop sharing** button, which has replaced the **Share this app content** button and also available on the top of the shared content as well.

![Content being shared in the meeting from the embedded app](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt07080498b6d514d0/642445cbb57cb810acb799c1/6.png)

The initiator app calls [clearPresentationUrl()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+clearShareUrl) to hide the **Share in meeting** button.

```javascript
meeting.clearPresentationUrl();
```

Notes:

* Although you can show both  **share this app content** and **Open for all** buttons on your app, but you can only use one at a time.
* The meeting host or co-host(s) will see the **Stop sharing** button when a sharing session is in progress, even if they did not click **Share in meeting** to start the session. This provides hosts with the ability to end a sharing sessions even if they didn't start it themselves.
* If screen share is already running in a meeting and another participant tries to screen share a content, they will be presented with the below confirmation message before swaping the shared content.
![Sharing a app when already screen share is in progress confirmation](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte310f9deed2c7dde/642445cbcfb44c109a1d5ed5/5.png)



## In-Space App Experience

The same initiator app can be used for both meetings and spaces, or you can specify a unique URL for each context (see [Creating your Embedded App](https://developer.webex.com/docs/embedded-apps-guide#creating-your-embedded-app)). There are some differences in the user experience of in-space compared to in-meeting apps to consider, as discussed below.

The screenshot below is of the initiator app open in a Webex messaging space. As with the in-meeting experience the user enters the poll questions and clicks **Create poll** which invokes `setShareUrl()`, causing an **Add to tab** button to appear.

![Add to Tab button in Space](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6396c3e8bdfa84c5/617766b4c84e4d1bb61ddb3b/space-add-to-tab.png)

Clicking **Add to tab** adds the specified URL as a tab to the space, as shown below. At the time the initiator app window closes. For this reason the in-space app design is slightly different than the in-meeting version: the poll results are provided in a separate tab of the shared app rather than in the initiator app.

![App added as tab to space](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltdd46e8afb5235e40/617766edb7799c1a3543c704/app-added-to-tab.png)

A feature unique to in-space apps is that you can optionally pass `setShareUrl()` the URL of a version of the shared app that's meant for use outside of the Webex client. For example, the following call to `setShareUrl()` includes the external URL `"https://www.example.com/poll_123_ext"` for the poll.

```javascript
app.setShareUrl("https://www.example.com/poll_123", "https://www.example.com/poll_123_ext", "Proposal Poll"`
```

The external URL is exposed to users via the **Open in browser** and **Copy URL** space tab menu items, as discussed in [Space tab menu items](https://developer.webex.com/docs/embedded-apps#space-tab-menu-items).

![Space tab menu](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt0c8a8c4f4e3fff3d/617767bf99dfaf274905ca64/in-space-tab-menu.png)

To clear the shared URL the initiator app calls [clearShareUrl()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+clearShareUrl).

```javascript
app.clearShareUrl();
```

### Space Tab Menu Items
<a id="space-tab-menu-items"></a>

The following lists the menu items displayed for an embedded app's space tab. Note that some of the menu items are only available to space moderators, as noted.

* **Expand** &mdash; Opens embedded app in a new window.
* **Copy link** &mdash; Copies external URL of embedded app to the clipboard. Only appears if a URL was provided as the second parameter to the [setShareUrl()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+setShareUrl) method call.
* **Open in browser** &mdash; Opens embedded app in the system's default web browser. Only appears if a URL was provided as the second parameter to the [setShareUrl()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+setShareUrl) method call.
* **Edit** &mdash; Opens a dialog where a user can edit the name the embedded app's tab. In moderated spaces, only moderators can edit an app; in unmoderated spaces any user can edit an app.
* **View information** &mdash; Lists basic information about the embedded app, including its URL, the user who added the app to the Space, the last edited date and the user who made the most recent edits.
* **Remove** &mdash; Removes the app from the Space. In moderated spaces, only moderators can remove apps; in unmoderated spaces any user can remove an app.

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

## Share a Link to a Sidebar App

Users can share a deep link to an approved sidebar app from the Webex App for desktop:

1. Open the app from the Webex App sidebar.
2. Open the app menu and select **Copy link**.
3. Paste the link wherever you want to share or save it, including outside Webex.

When a recipient clicks the link, Webex opens the app directly in the sidebar if the app is approved and available to that recipient. Otherwise, Webex displays an error. The **Copy link** option is not available for in-development apps. Copied links always open the sidebar context; this feature does not create links for the in-meeting or messaging contexts.

Webex generates links in the following format:

```text
webexteams://im?embeddedapp=<groupId>&context=sidebar
```

The `groupId` value is the app extension's internal group identifier, not the app ID shown in the Developer Portal. Use the link generated by **Copy link** instead of constructing the URL manually.

## More Information

For more information about developing embedded apps, see the following topics:

- [Developer quick start](https://developer.webex.com/docs/embedded-apps-guide#developer-quick-start) &mdash; Walks you through the steps to create your first embedded app and test it with the **Open for all** feature in a meeting, and the **Add to tab** feature in a space.
- [Responding to events](https://developer.webex.com/docs/embedded-apps-guide#responding-to-events) &mdash; Explains how to register event handlers for various events generated by the framework.
- [Embedded Apps Framework API Reference](https://developer.webex.com/docs/embedded-apps-api-reference) &mdash; Complete API reference for embedded app developers.
- [Design guidelines and considerations](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings) for [in-meeting](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings) and [in-space](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces) embedded apps.
- [Embedded Apps Framework Sidebar API Quick Start](https://developer.webex.com/docs/embedded-apps-framework-sidebar-api-quick-start) &mdash; Walks you through using the Sidebar API to create Always On Embedded Apps that can respond to various events.
