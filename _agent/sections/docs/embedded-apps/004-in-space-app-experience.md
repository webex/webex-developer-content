---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- In-Space App Experience
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
