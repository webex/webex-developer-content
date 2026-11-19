---
type: Guide
title: Embedded Apps for Webex Devices Developer Guidelines
display_title: Devices
canonical_url: https://developer.webex.com/docs/embedded-apps-for-webex-devices
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/embedded-apps-for-webex-devices)

## Introduction

This document provides design and experience guidelines for embedded apps running on Webex Devices. It provides the following levels of guidance:

 - ­­­**Requirements** that in-meeting embedded apps must meet to be approved for inclusion on Webex App Hub.
    **IMPORTANT**: Webex App Hub is not supported for Webex for Government (FedRAMP).
* **Recommended design guidelines** that when implemented provide a great experience for users. While not explicitly required, apps that do not incorporate the recommended guidelines may not be approved if it is determined they provide a poor user experience.
* **Good-to-have design guidelines** that when incorporated provide an enhanced user experience, both within the app itself and the larger Webex context.

**[Submit your idea](https://app.smartsheet.com/b/form/ded8205ca16b47b8a77f99358c934d67)** for an embedded app on Webex Devices! 

## About Webex Devices

Webex video devices are purpose built for video conferencing and visual collaboration for effortless new ways to connect with your team, share your ideas, and express yourself. Webex devices are designed to provide high-quality meeting experiences without needing a laptop.

Cisco makes devices to meet the needs of today’s hybrid digital world: providing solutions for all types of meeting spaces, as well as home offices. As work is hybrid, employees need access to people, content and applications no matter where they conduct work. To help address those needs, applications can be embedded in Webex and now Webex Devices to enable rich collaboration. To learn more about Webex devices, please visit [Project Workplace](https://projectworkplace.cisco.com). 

You use the [Webex Embedded App SDK](https://developer.webex.com/docs/embedded-apps-guide) to create apps that run on Webex devices. This guide provides additional guidelines and requirements to consider when creating apps for Webex Devices. This document also provides [unique requirements and limitations](https://developer.webex.com/docs/embedded-apps-for-webex-devices#technical-requirements-and-limitations) for embedded apps on Webex Devices.

## Supported Devices

<table>
    <colgroup>
        <col style="width: 24%" />
        <col style="width: 24%" />
        <col style="width: 25%" />
        <col style="width: 25%" />
    </colgroup>
    <thead>
        <tr class="header">
            <th><strong>Device</strong></th>
            <th><strong>Description</strong></th>
            <th><strong>More information</strong></th>
            <th><strong>Data sheet link</strong></th>
        </tr>
    </thead>
    <tbody>
        <tr class="odd">
            <td>
                <p>Webex Board Pro</p>
                <p><img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte932a7d53f9d6a0c/6238e474f243f804238b6ec2/board-pro.png"
                        alt="Webex Board Pro" /></p>
            </td>
            <td>All-in-one touch device for video conferencing, digital whiteboarding and team collaboration in a
                meeting room.</td>
            <td>Visit <a href="https://projectworkplace.cisco.com/products/webex-board-pro">here</a></td>
            <td><a href="https://www.cisco.com/c/en/us/products/collateral/collaboration-endpoints/webex-board/webex-board-pro-ds.html">Board Pro</a></td>
        </tr>
        <tr class="odd">
            <td>
                <p>Webex Board</p>
                <p><img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta083fcbd5c04edbc/6238a139d648da17618c9498/board.png"
                        alt="Webex Board Pro" /></p>
            </td>
            <td>First generation Webex Board for an all-in-one meeting room experience.</td>
            <td>See above for the all-new Board Pro. </td>
            <td>
            <ul>
                <li><a href="https://www.cisco.com/c/en/us/products/collateral/collaboration-endpoints/webex-board/datasheet-c78-741939.html">55" data sheet</a></li>
                <li><a href="https://www.cisco.com/c/en/us/products/collateral/collaboration-endpoints/webex-board/datasheet-c78-741937.html">70" data sheet</a></li>
                <li><a href="https://www.cisco.com/c/en/us/products/collateral/collaboration-endpoints/webex-board/datasheet-c78-741522.html">85" data sheet</a></li> 
            </ul>
            </td>
        </tr>
        <tr class="even">
            <td>
                <p>Desk Pro</p>
                <p><img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1e04150046ec0029/6238e96d8ee56a1b0ac2fae7/collaboration-endpoints-webex-desk-pro.jpeg" 
                        alt="Desk Pro image" /></p>
            </td>
            <td>All-in-one collaboration device for your desk or huddle room.</td>
            <td>
            Visit <a href="https://projectworkplace.cisco.com/products/cisco-webex-desk-pro">here</a> 
            </td>
            <td><a href="https://www.cisco.com/c/en/us/products/collaboration-endpoints/webex-desk-pro/datasheet-c78-743105.html">Desk Pro</a></td>
        </tr>
        <tr class="odd">
            <td>
                <p>Desk</p>
                <p><img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd35d857f3cb661ae/6238e7dff243f804238b6eda/desk.png"
                        alt="Desk Webex Device" />
                </p>
            </td>
            <td>All-in-one collaboration device for every desk; at home or in the office.</td>
            <td>
            Visit <a href="https://projectworkplace.cisco.com/products/cisco-webex-desk">here</a> 
            </td>
            <td><a href="https://www.cisco.com/c/en/us/products/collateral/collaboration-endpoints/webex-desk-series/webex-desk-ds.html">Desk</a></td>
        </tr>
        <tr class="even">
            <td>
                <p>Desk Mini</p>
                <p><img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt654085eb899b9326/6238e765815d0316181c5c86/desk-mini.png"
                        alt="Desk Mini" /></p>
            </td>
            <td>A portable all-in-one desk device designed for taking meetings in any room.</td>
            <td>
            Visit <a href="https://projectworkplace.cisco.com/products/desk-mini">here</a> 
            </td>
            <td><a href="https://www.cisco.com/c/en/us/products/collateral/collaboration-endpoints/webex-desk-mini/webex-desk-mini.html">here</a></td>
        </tr>
    </tbody>
</table>

## User Experience on Webex Devices

Embedded Apps are available in Webex meetings and Webex spaces. Apps can currently only be shared (via **Open Together** or **Add to Tab**) from the desktop Webex app, but any supported device participating in the meeting will open the app whenever a session is initiated. Apps can be displayed in two views: 

* **Panel view** &mdash; This is the default view when an embedded app is opened or shared. The panel width is fixed.

    ![Panel view](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt08741c9b7e46e80f/6238a1393dcb491c40ccb12f/panelview.png)

* **Stage view** &mdash; Users can expand the app to fill the stage.

    ![Stage view](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt19839dc13e97048d/6238a139815d0316181c5ba9/stageview.png)

The following buttons let users switch between the two views and close the embedded app.

<table>
<tbody>
<tr>
<td> Go from panel view to stage view      </td>
<td><img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltba987b6ccea251be/6238a34ee8be663d8c157d70/expander.png" width="150px" alt="Expander button" />  </td>
</tr>
<tr>
<td>Go from stage view to panel view    </td>
<td>    <img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7d9a71acd02b9dd4/6238a34e58d228056c02695c/panelview-btn.png" width="150px" alt="Collapse button" />   </td>
</tr>
<tr>
<td>Close Embedded App (only locally)    </td>
<td>  <img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt213a66c6b3cd3852/6238a34e4dd07a3d8e130197/close-btn.png" width="150px" alt="Close button" /></td>
</tr>
</tbody>
</table>

For in-meeting apps, if an app is closed it can be re-opened from the **Apps** button as long as the sharing session is still in progress.

![Apps button](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt738acf07d2a46e39/6239e3d5f174ad4de515a2ea/apps-btn.png)

## App Submission and Approval

Only embedded apps that have approved for Webex AppHub can be used on Webex Devices. To have your app approved please start by reviewing the design requirements and recommendations in this document. If your app is suitable for Webex Devices and can work well within the [technical requirements](https://developer.webex.com/docs/embedded-apps-for-webex-devices#technical-requirements-and-limitations) please [submit your idea for consideration](https://app.smartsheet.com/b/form/ded8205ca16b47b8a77f99358c934d67) and we will get to back to you with next steps. 

## Optimizing the Experience for Webex Devices

Embedded apps can check the value of [webex.application.deviceType](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+deviceType) in the Embedded App SDK to see what type of device the application is running on. This property currently returns the string `"ROOM_SYSTEM_PERSONAL"` when running on a Webex Device. Information about the exact device model can be found in the [webex.application.about](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+about) property. This makes it possible to adapt the functionality of your app specifically for the Webex Device, if needed.

## Technical Requirements and Limitations

This section describes design and development considerations unique to creating embedded apps for Webex Devices.

- [Testing and Debugging](https://developer.webex.com/docs/embedded-apps-for-webex-devices#testing-and-debugging)
- [User Experience and Navigation](https://developer.webex.com/docs/embedded-apps-for-webex-devices#user-experience-and-navigation)
- [Hardware](https://developer.webex.com/docs/embedded-apps-for-webex-devices#hardware)
- [Unsupported web features](https://developer.webex.com/docs/embedded-apps-for-webex-devices#unsupported-web-features)
- [Multimedia](https://developer.webex.com/docs/embedded-apps-for-webex-devices#multimedia)

<a id="testing-and-debugging"></a>

### Testing and Debugging

Unlike on the Webex App for desktop systems, Webex Devices don't currently provide a way to [enable developer tools](https://developer.webex.com/docs/embedded-apps-guide#enabling-developer-tools-in-meeting-client-and-webex) inor the "Refresh" button to in the embedded webview to reload your app from its source URL. 

To test changes you've deployed to your embedded app once you've started it on a Webex Device you need to manually restart the app. Webex will reload your app's updated assets from your web host.

<a id="user-experience-and-navigation"></a>

### User Experience and Navigation

* Embedded apps on Webex devices can currently be used to only receive content shared by other meeting participants. In other words, embedded apps on Webex Devices cannot call [setShareUrl()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+setShareUrl) to share content with other meeting participants via the **Open Together** feature. 
* All user interaction must be done through [touch events](https://developer.mozilla.org/en-US/docs/Web/API/Touch_events/Using_Touch_Events).
* Using `window.open()` to open external browser windows is not supported.
* Browser history navigation (for example, "back" or "forward" buttons) are not available. However, apps can use the JavaScript [History API](https://developer.mozilla.org/en-US/docs/Web/API/History_API) to move forward or back in the user's navigation history.
* The device keyboard is only available for text input fields on the touch screen (no keyboard shortcuts).
* Webex Devices do not support the ability to "Refresh" (reload) the embedded app from it's original URL.

<a id="hardware"></a>

### Hardware

The web engine used to render embedded apps on device is based on the Chromium/Qt WebEngine with V8 JavaScript. The current version is Chromium 77, with ongoing work to support Chromium 87.

<a id="unsupported-web-features"></a>

### Unsupported web features

The following web features are not supported by the Webex Devices web engine:

* PDF rendering
* File upload and download
* WebGL
* Session cookies

<a id="multimedia"></a>

### Multimedia

* Audio and video playback is supported. It is recommended to limit video resolution to 1080p resolution to ensure smooth playback.


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

## Recommended Design Guidelines

Embedded apps are expected to follow the recommended design guidelines discussed below. While not required for approval, apps that do not incorporate these recommended guidelines may not be approved for App Hub if the reviewer determines that the app provides a poor user experience.

Except where noted, the recommended design guidelines apply to both in-meeting and in-space apps.

* [Open Together Experience Recommendations](https://developer.webex.com/docs/embedded-apps-for-webex-devices#open-together-experience-recommendations)
* [Focus on Simplified Workflows and Use Cases](https://developer.webex.com/docs/embedded-apps-for-webex-devices#focus-on-simplified-workflows-and-use-cases)
* [Respond to User's Color Theme Preference](https://developer.webex.com/docs/embedded-apps-for-webex-devices#respond-to-user-s-color-theme-preference)
* [Sign-in Guidelines](https://developer.webex.com/docs/embedded-apps-for-webex-devices#sign-in-guidelines)

<a id="open-together-experience-recommendations"></a>

### Open Together Experience Recommendations

The following are recommendations for the Open Together experience:

* Apps should avoid including hyperlinks to parts of the application that weren't intended to be part of the embedded app experience, or take the user to an unknown part of the app.
* If certain Open Together workflows are not enabled in the app, the developer should minimally provide the user with next steps through a text banner.

<a id="focus-on-simplified-workflows-and-use-cases"></a>

### Focus on Simplified Workflows and Use Cases

Developers should not try to repurpose or replicate their entire existing web app as an embedded app. Embedded apps benefit users with simplified use cases and workflows that add value to a Webex meeting or messaging space.

<a id="respond-to-user-s-color-theme-preference"></a>

### Respond to User's Color Theme Preference

Webex users can select a light or dark theme for the Webex or Meeting Center app. To provide the best user experience, embedded apps should be responsive to the user's theme preference and provide both light and dark color themes. Minimally, an app's light theme should provide dark-colored text on a light-colored background, while the dark them should display light-colored text on a dark-colored background.

![Slido app adpating to light and dark color themes in Webex app](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2b8331f339dbb0b6/61b90cc5c52c5b292ce22f36/slido-light-dark.png)

<a id="sign-in-guidelines"></a>

### Sign-in Guidelines

Apps that require user accounts should make the sign-up and sign-in processes as easy as possible for the user. Specifically, apps should incorporate the following:

* App recipients should have the same or similar sign-up and sign-in experience as the app initiator.
* Apps should use cookies and local storage to persist a user's log-in information, so that users do not need to log in each time they open a space tab or join an Open Together session. The embedded app version of your service or application should provide the same sign-in or session persistence as the browser-based version. See [Using Cookies and Web Storage](https://developer.webex.com/docs/embedded-apps-guide#cookies_local_storage) in the Embedded Apps developer guide for more information.
* Apps should use third-party identity providers for user sign-in only when necessary.

## Good-to-Have Design Guidelines

The following suggestions provide an enhanced user experience both within your app and in the larger Webex context. Incorporating these suggestions is optional and will not block app approval if not implemented.

### Provide a "Freemium" Model for First-time Users

Apps that require users to create an account and select a pricing plan should provide a "freemium" model to allow first-time users an easy sign-up experience. Apps can use the participant's [user ID](https://developer.webex.com/docs/embedded-apps-api-reference#type-definitions) to create a placeholder association between the user and the current app session. This ID is guaranteed to be unique regardless of whether the app has access to the user's personally identifiable information (PII).
