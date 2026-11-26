---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- In-Meeting App Experience - Interactive experience
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
