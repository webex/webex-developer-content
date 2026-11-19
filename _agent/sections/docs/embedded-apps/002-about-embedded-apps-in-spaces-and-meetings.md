---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- About Embedded Apps in Spaces and Meetings
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

## About Embedded Apps in Spaces and Meetings

This section provides a high-level overview of the user experience for using embedded apps in Webex meetings and spaces. In each case the process starts with a meeting participant clicking the **Apps** button (in a meeting) or tab (in a space) to view the list of available apps, and then opening your app.

![Buttons to open list of embedded apps in meeting and spaces](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc3e0083aadb688f5/617764eab685fa1bb581b759/app-btns.png)

The app the user opens is called the _initiator app_ and is the one specified by your app's "Start Page URL" when you [create a new embedded app in the Developer Portal](https://developer.webex.com/docs/embedded-apps-guide#creating-your-embedded-app). The purpose of the initiator app is to share the URL of an app &mdash; the _shared app_ &mdash; that is either [opened with meeting participants](https://developer.webex.com/docs/embedded-apps#inmeeting-app-experience) in real-time, or [added as a tab to a space](https://developer.webex.com/docs/embedded-apps#inspace-app-experience).


This URL is passed the framework's [setShareUrl()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+setShareUrl) method, which causes an **Open for all** or **Add to tab** button to appear in the initiator app's window, depending if the app is running in a meeting or space, respectively. Read more the user experience of [in-meeting](https://developer.webex.com/docs/embedded-apps#inmeeting-app-experience) and [in-space](https://developer.webex.com/docs/embedded-apps#inspace-app-experience) embedded apps.
