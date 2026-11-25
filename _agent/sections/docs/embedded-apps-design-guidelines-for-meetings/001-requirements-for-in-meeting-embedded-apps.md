---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Requirements for In-Meeting Embedded Apps
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings). [Full Markdown](../../../../docs/embedded-apps-design-guidelines-for-meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

This document provides design and experience guidelines for embedded apps running in a Meeting, specifically:

 - **Requirements** that in-meeting embedded apps must meet to be approved for inclusion on [Webex App Hub](https://apphub.webex.com).
 - **Recommended design guidelines** that when implemented provide a great experience for users of in-meeting apps. While not explicitly required, apps that do not incorporate the recommended guidelines may not be approved if it is determined they provide a poor user experience.
 - **Good-to-have design guidelines** that when incorporated into in-meeting apps provide an enhanced user experience, both within the app itself and the larger Webex context.



> **Warning**
>
> Webex App Hub is not supported for Webex for Government (FedRAMP).




See [Embedded Apps Design and Experience Guidelines for Messaging](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces) for guidelines related to messaging-based apps.

## Selected section

## Requirements for In-Meeting Embedded Apps

This section describes design and user experience requirements for in-meeting embedded apps.

* [Open For All User Experience](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#open-together-experience)
* [Responsive Layout](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#responsive-layout)
* [Platform and Device Support](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#platform-and-device-support)
* [Use of Pop-up Windows](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#use-of-pop-up-windows)
* [Access to User Information](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#access-to-user-information)
* [First-time User Experience](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#first-time-user-experience)
* [Legibility in Light and Dark Modes](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#legibility-in-light-and-dark-modes)
* [Other](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#other)

<a id="open-together-experience"></a>

### Open For All Experience

The ability to share content with meeting participants using the **Open for All** feature is the at the heart of the embedded app user experience. The following requirements are to ensure that an app's Open for All workflows are clear and intuitive to users.

* Apps must be optimized for the two Open for All personas: the app initiator who starts the Open for All session, and the app recipients who interact with the opened app.
* An app's primary use cases and workflows must provide the app initiator with the ability to start an Open for All session. Apps must not contain workflows that leaves the app initiator "stranded" and unable to start an Open for All session.
* If an Open for All workflow involves multiple user steps, apps must provide clear and consistent navigation between steps. App initiators must be able to go back or forward in an Open for All workflow to select different content to share with app recipients.
* If an app enables the Open for All button it must always provide the content that will be shared with app recipients. Open for All must not be used on Login Pages or other views where there is nothing for the app initiator to share.
* While an Open for All session is in progress, app recipients must be presented with the same view or content that the app initiator intended to share. If the app recipient navigates away from the intended view, the app must provide a way for the user to return to the intended experience.

* App recipient functionality and experience must be verified on Android and iOS devices. Recipients must be able to see and interact with the shared content.
<a id="responsive-layout"></a>

### Responsive Layout

In-meeting apps must optimize their layouts to their default viewports. As detailed below, there are unique viewport sizes for apps running in the App panel (where apps open by default) and in the external window that the user can pop out.

Embedded apps can be configured to open in either in the app panel, or the main meeting view.

* [App Panel](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#app-panel)
* [Main View](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#main-view)
* [Pop Out Window](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#pop-out-window)
* [Mobile Devices](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#mobile-devices)
* [Scrolling Ability](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#scrolling-ability)

<a id="app-panel"></a>

### App Panel

By default, apps are launched into the App panel with a viewport of **360x576px**. Apps must be optimized for this viewport. Apps can optionally be configured to open in the [main meeting view](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#main-view).

![Default window size for in-meeting app](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7440c609e2c2d081/61b8ebe2d73c783f9a3d1591/meeting-receiver-view.png)

When the **Open for all** button is enabled the app's available viewport is **360x480px**. Apps must be optimized for this smaller viewport.

![Default window size when Open for all** is enabled](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2b096e38c2aa6be7/61b8ebe2e5a70e7d5276af31/meeting-initiator-view.png)

When **Open for all** is not enabled, app initiators and recipients can stretch the width of the App panel up to a maximum of **604x576px.** Apps must be optimized for these dimensions.

![Maximum stretched window size for in-meeting app](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1f884969e21a464e/61b8ebe2d628d527ff43ff40/in-meeting-app-panel-full-size.png)

When **Open for all** is enabled the app's viewport is **604x480px**. Apps must be optimized for these dimensions.

![Maximum stretched window size for in-meeting app when Open for all** is enabled](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt98d6cd7bebda0fd4/61b8ebe295cb603e6b5cbcc5/meeting-stretch-width.png)

<a id="main-view"></a>

### Main View

In-meeting embedded apps have a Layout Preference [configuration option](https://developer.webex.com/docs/embedded-apps-guide#embedded-app-configuration-options) that determines if shared content opens for meeting participants in the side panel or in the main meeting view at default size of **1264x490**. Apps launched into the main view must be optimized for this viewport.

![Main view](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd122e4c7e93ddc1c/62aa0b0fb53bb658a3927211/stageview-receiver.png)

<a id="pop-out-window"></a>

### Pop Out Window

The user can click the expand icon in the app's title bar to pop out the app into a separate window at a default size of **720x510px**. Apps must be optimized for this default window size. Users can resize the pop-out window to any size, so apps must be responsive to other viewport sizes, including full screen.

![In-meeting default pop-out window size](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt370df9d61a52d771/61b8ebe395cb603e6b5cbcc9/meeting-pop-out-window.png)

<a id="mobile-devices"></a>

### Mobile Devices

For in-meeting apps, app recipients can view shared content on mobile devices. Apps must optimize their layouts for common mobile device screen sizes and orientations. (Users cannot initiate **Open for all** sessions on mobile devices.)

![Example mobile device](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt510a14054f301dc2/61b9027a8f8a44201b510dce/mobile_app.jpg)

<a id="scrolling-ability"></a>

### Scrolling Ability

Apps must provide users with the ability to easily scroll the app's visible content. By default, in-meeting apps open in the App panel, which may contain other open panels (such as Chat or Participants panel, for example) thereby reducing the app's available screen area. For example, in the screenshot below the Slido app is open and is sharing the available space with other panels. Users must be able to access app content in this view by scrolling vertically.

![Screenshot of many panels open in App panel, requiring user to scroll vertically](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltda88368cd7f5ad8f/61b8ebe1121d687d6e01768d/many-panels-open.png)



<a id="platform-and-device-support"></a>

### Platform and Device Support

Apps must be tested and verified to function as expected on all supported desktop systems and devices, including Windows and MacOS.

Apps that are intended to be used on Webex Devices (such as the DX80 or DeskPro) must be optimized for a touch-screen experience.

<a id="use-of-pop-up-windows"></a>

### Use of Pop-up Windows

In general, apps should limit their use of pop-up windows created via JavaScript. In particular:

* Pop-up windows created via the `window.open()` JavaScript method must not be used for primary app workflows or experiences.

* Use of pop-ups must be limited to entering sign-in credentials, or displaying error messages or notification messages, only. Pop-up windows must be closed once the user has completed the sign-in process or acknowledged the notification or error message.

<a id="access-to-user-information"></a>

### Access to User Information

* Apps must not require a user to provide a phone number to enable use of the app. If the app solicits personal information from the user, it must not spam users with that information.
* Apps must not be dependent on access to a user's personally identifiable information (PII) to function properly. By default, access to PII in embedded apps is not enabled and apps must be able to function without access to PII. For more information, see [Access to Personally Identifying Information](https://developer.webex.com/docs/embedded-apps-guide#personally-identifiable-information-pii-and-embedded-apps).
* Embedded apps may obtain user information via an [Integration](https://developer.webex.com/docs/integrations) with [Webex APIs](https://developer.webex.com/docs/getting-started), but integrations should limit the [requested scopes](https://developer.webex.com/docs/integrations#scopes) to the minimum their application needs to function. For more information, see [Combined Webex Developer Solutions]() in the Embedded Apps Developer Guide. 

<a id="first-time-user-experience"></a>

### First-time User Experience

The following are requirements for the first-time user experience.

* Apps must be easy and intuitive for first-time users and provide clear call-to-actions (CTAs) in onboarding workflows.
* If a user is required to sign-in to use the app, all available sign-in methods in the app must be functional.
* If the user needs to first sign-up (create an external account) before using the app, the app must provide guidance on how users need to complete that process.

<a id="legibility-in-light-and-dark-modes"></a>

### Legibility in Light and Dark Modes

The Webex app provides users the option to enable dark or light mode for the user interface. All embedded app text and content must be visible, legible, and actionable in both color modes. In particular, apps must not have transparent backgrounds, which can make text illegible in dark mode.

<a id="other"></a>

### Other

* If an app encounters an error condition that it cannot recover from, it must provide users with graceful exit points and appropriate messaging about the error state.
* Apps that require a user to sign-in must also provide a way for the user to sign-out.
* Apps must not display advertisements. This requirement is evaluated on a per-app basis and depends on the situation (for example, if an app's underlying business model is dependent on ads).
* Apps must not include links to extraneous pages where not actionable (for example, links to "About", "Careers", or social media sites) that would leave the user "stranded".
