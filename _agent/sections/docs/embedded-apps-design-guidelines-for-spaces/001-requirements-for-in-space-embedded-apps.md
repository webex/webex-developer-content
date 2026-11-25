---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Requirements for In-Space Embedded Apps
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces). [Full Markdown](../../../../docs/embedded-apps-design-guidelines-for-spaces.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

This document provides design and experience guidelines for embedded apps running in a Messaging space, specifically:

- ­­­**Requirements** that in-space embedded apps must meet to be approved for inclusion on Webex App Hub.
* **Recommended design guidelines** that when implemented provide a great experience for users of in-space apps. While not explicitly required, apps that do not incorporate the recommended guidelines may not be approved if it is determined they provide a poor user experience.
* **Good-to-have design guidelines** that when incorporated into embedded apps provide an enhanced user experience, both within the app itself and the larger Webex context.



> **Warning**
>
> Webex App Hub is not supported for Webex for Government (FedRAMP).



See [Embedded Apps Design and Experience Guidelines for Meetings](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings) related to meeting-based apps.

## Selected section

## Requirements for In-Space Embedded Apps

This section describes design and user experience requirements for in-space embedded apps.

* [Add Tab to Space Experience](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces#add-tab-to-space-experience)
* [Responsive Layout](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces#responsive-layout)
* [Platform and Device Support](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces#platform-and-device-support)
* [Use of Pop-up Windows](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces#use-of-pop-up-windows)
* [Access to User Information](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces#access-to-user-information)
* [First-time User Experience](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces#first-time-user-experience)
* [Legibility in Light and Dark Modes](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces#legibility-in-light-and-dark-modes)
* [Other](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces#other)

<a id="add-tab-to-space-experience"></a>

### Add Tab to Space Experience

In a messaging space, the app initiator selects or specifies the content to share, and then clicks **Add to Tab** to add the specified content as a space tab. For a detailed overview of the in-space experience, see [In-Space App Experience](https://developer.webex.com/docs/embedded-apps#inspace-app-experience) in the Embedded Apps documentation.

The following requirements are to ensure that an app's Add to Tab workflows are clear and intuitive to users.

* Apps must have at least one workflow that results in **Add to Tab** appearing.
* Once an app is added as a tab, all members of the space must see the same content that was intended to be shared.
* If users are required to sign-in or sign-up before using the app, the app must present the user's initial view or context when they complete the sign-in or sign-up process.
* The shared app's main content and features must be presented in the space tab, not in external pop-up windows (see [Use of Pop-up Windows](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces#use-of-pop-up-windows)). Pop-up windows must be used only for specific actions, such as sign-in or sign-up workflows, and must be closed after the action is complete.
* Apps added to a tab must provide a consistent experience each time a user opens the app. Apps should use [local storage](https://developer.webex.com/docs/embedded-apps-guide#cookies_local_storage) to maintain state between sessions.

<a id="responsive-layout"></a>

### Responsive Layout

In-space apps must optimize their layouts to the default window sizes in which they run. By default, the app used to add a space tab opens in a **580x597px** window. The app's layout must be optimized for this viewport.

![Default in-space window size for in-space app used to add tab without open for all enabled](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7aaed3ecd72c97e7/61b8ebe1191c5560467dbfc6/in-space-app1-default.png)

When the **Add to Tab** button is enabled, the available screen area is **580x525px**. The app's layout must be optimized for this view.

­­![Default in-space window size for in-space app used to add tab with open for all enabled](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt19f29660e97b9733/61b8ebe2191c5560467dbfca/in-space-app-picker.png)

The default dimensions of an app that has been added to a space is **780x520px**. App layouts must be optimized for this initial viewport size.

![Default size of in-space app that's been added to a tab](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7f34f9f1be47a69c/61b8ebe35b7db17e976062c8/in-space-tab.png)

The user can pop out the space tab into an external window with a default size of **788x488px**. App layout must be optimized for this initial pop-out window size.

![Default size of in-space app when popped out into a separate window](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd68442ce26120e95/61b8fe57d628d527ff43ff90/in-space-pop-out.png)

Users can resize the pop-out window to any size, so apps must be responsive to other viewports, including full screen.

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

<a id="add-tab-to-space-experience"></a>
