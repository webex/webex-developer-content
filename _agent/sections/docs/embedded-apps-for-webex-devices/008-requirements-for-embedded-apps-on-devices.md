---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-for-webex-devices
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Requirements for Embedded Apps on Devices
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-for-webex-devices). [Full Markdown](../../../../docs/embedded-apps-for-webex-devices.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Technical Requirements and Limitations](007-technical-requirements-and-limitations.md)

## Selected section

## Requirements for Embedded Apps on Devices

This section describes design and user experience requirements for in-meeting embedded apps.

* [Open Together Experience](https://developer.webex.com/docs/embedded-apps-for-webex-devices#open-together-experience)
* [Responsive Layout](https://developer.webex.com/docs/embedded-apps-for-webex-devices#responsive-layout)
* [Platform and Device Support](https://developer.webex.com/docs/embedded-apps-for-webex-devices#platform-and-device-support)
* [Touch Screen Support](https://developer.webex.com/docs/embedded-apps-for-webex-devices#touch-screen-support)
* [Scrolling Ability](https://developer.webex.com/docs/embedded-apps-for-webex-devices#scrolling-ability)
* [Access to User Information](https://developer.webex.com/docs/embedded-apps-for-webex-devices#access-to-user-information)
* [First-time User Experience](https://developer.webex.com/docs/embedded-apps-for-webex-devices#first-time-user-experience)
* [Legibility in Light and Dark Modes](https://developer.webex.com/docs/embedded-apps-for-webex-devices#legibility-in-light-and-dark-modes)
* [Other](https://developer.webex.com/docs/embedded-apps-for-webex-devices#other)

<a id="open-together-experience"></a>

### Open Together Experience

Open Together is the heart of the in-meeting app experience. The following requirements are to ensure that an app's **Open Together** workflows are clear and intuitive to users.



> **Info**
>
> Embedded apps on Webex Devices cannot initiate **Open Together** sessions in a Webex Meeting, they can only act as recipients of content shared by other meeting participants.



The following guidelines apply only to recipients of on Open Together session:

* Apps must be optimized the app recipient who interacts with the opened app.
* While an Open Together session is in progress, app recipients must be presented with the same view or content that the app initiator intended to share. If the app recipient navigates away from the intended view, the app must provide a way for the user to return to the intended experience.

<a id="responsive-layout"></a>

### Responsive Layout

Apps must optimize their layouts to their default viewports. As detailed below, there are unique viewport sizes for apps running in the App panel (where apps open by default) and in full-screen mode that the user can enable.

* [App Panel](https://developer.webex.com/docs/embedded-apps-for-webex-devices#app-panel)
* [Stage View](https://developer.webex.com/docs/embedded-apps-for-webex-devices#stage-view)

<a id="app-panel"></a>

### App Panel

By default, apps are launched into the App panel with a fixed viewport. Apps must be optimized for this viewport. Users cannot resize the App panel.

![Default window size in App panel](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt08741c9b7e46e80f/6238a1393dcb491c40ccb12f/panelview.png)

<a id="stage-view"></a>

### Stage View

Users can tap the expand icon in the app's title bar to make the window fill the device's screen. Apps must adapt their layout responsively to this viewport.

![Full screen window](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt19839dc13e97048d/6238a139815d0316181c5ba9/stageview.png)


<a id="touch-screen-support"></a>

### Touch Screen Support

All user interaction on Webex Devices must be done through [touch events](https://developer.mozilla.org/en-US/docs/Web/API/Touch_events/Using_Touch_Events). App must be optimized for a touch-screen experience.

<a id="scrolling-ability"></a>

### Scrolling Ability

Apps must provide users with the ability to easily scroll the app's visible content. By default, in-meeting apps open in the App panel, which may contain other open panels (such as Chat or Participants panel, for example) thereby reducing the app's available screen area. For example, in the screenshot below the Slido app is open and is sharing the available space with other panels. Users must be able to access app content in this view by scrolling vertically.

![Screenshot of many panels open in App panel, requiring user to scroll vertically](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltda88368cd7f5ad8f/61b8ebe1121d687d6e01768d/many-panels-open.png)



<a id="platform-and-device-support"></a>

### Webex Device Support

Apps must be tested and verified to function as expected on all supported Webex Devices. See [Supported Devices](https://developer.webex.com/docs/embedded-apps-for-webex-devices#supported-devices) for links to data sheets providing screen size information for each device.

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

<a id="other"></a>

### Other

* If an app encounters an error condition that it cannot recover from, it must provide users with graceful exit points and appropriate messaging about the error state.
* Apps that require a user to sign-in must also provide a way for the user to sign-out.
* Apps must not display advertisements. This requirement is evaluated on a per-app basis and depends on the situation (for example, if an app's underlying business model is dependent on ads).
* Apps must not include links to extraneous pages where not actionable (for example, links to "About", "Careers", or social media sites) that would leave the user "stranded".
