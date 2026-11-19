---
type: Guide
title: Embedded Apps Design and Experience Guidelines for Sidebar | Consolidated Guide
display_title: Sidebar
canonical_url: https://developer.webex.com/docs/embedded-apps-design-and-experience-guidelines-for-sidebar
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/embedded-apps-design-and-experience-guidelines-for-sidebar)

Make sure your embedded app follows these best practices for a great user experience

---

This document provides design and experience guidelines for embedded apps running in the Sidebar of the Webex app, specifically:

- **Requirements** that sidebar embedded apps must meet to be approved for inclusion on [Webex App Hub](https://apphub.webex.com).
- **Recommended design guidelines** that when implemented provide a great experience for users of Sidebar apps. While not explicitly required, apps that do not incorporate the recommended guidelines may not be approved if it is determined they provide poor user experience.
- **Good-to-have design guidelines** that when incorporated into sidebar apps provide an enhanced user experience, both within the app itself and the larger Webex context.



> **Warning**
>
> Webex App Hub is not supported for Webex for Government (FedRAMP).



See [Embedded Apps Design and Experience Guidelines for Meetings](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings) for guidelines related to messaging-based apps.

See [Embedded Apps Design and Experience Guidelines for Messaging](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces) for guidelines related to messaging-based apps

See [Embedded Apps Design and Experience Guidelines for Devices](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-devices) for guidelines related to device-based apps

## Requirements for Sidebar Embedded Apps

This section describes design and user experience requirements for sidebar embedded apps.

- [Generic User Experience](https://developer.webex.com/docs/embedded-apps-design-and-experience-guidelines-for-sidebar#generic-user-experience)
- [Responsive Layout](https://developer.webex.com/docs/embedded-apps-design-and-experience-guidelines-for-sidebar#responsive-layout)
- [Platform and Device Support](https://developer.webex.com/docs/embedded-apps-design-and-experience-guidelines-for-sidebar#platform-support)
- [Use of Pop-up Windows](https://developer.webex.com/docs/embedded-apps-design-and-experience-guidelines-for-sidebar#use-of-pop-up-windows)
- [Access to User Information](https://developer.webex.com/docs/embedded-apps-design-and-experience-guidelines-for-sidebar#access-to-user-information)
- [First-time User Experience](https://developer.webex.com/docs/embedded-apps-design-and-experience-guidelines-for-sidebar#first-time-user-experience)
- [Legibility in Light and Dark Modes](https://developer.webex.com/docs/embedded-apps-design-and-experience-guidelines-for-sidebar#legibility-in-light-and-dark-modes)
- [Other](https://developer.webex.com/docs/embedded-apps-design-and-experience-guidelines-for-sidebar#other)

<a id="generic-user-experience"></a>

### Generic User Experience

- The Sidebar context is intended to provide a higher level app experience, rather than a context-specific instance of the app like in Meetings and Messaging. Consider including all the functionality that a user might need to access for the app from the initial view.
- If the app recipient navigates away from the intended view, the app must provide a way for the user to return to the intended experience.
- The app should be evaluated if it is intended to support event monitoring (for example, detecting incoming calls and executing a certain business logic), as well as whether Personally Identifiable Information (PII) should be enabled for the app. In general, apps intended for event monitoring will require PII enablement. Also, the app should be evaluated and designed to handle one call at a time or multiple calls based on the use case.
- If the app does support event monitoring, notifying the user about incoming calls can be provided with the following two options:
     1. Show the alert in the sidebar next to the app.
     2. Automatically pop open a window in the system’s web browser with the app open to the desired location.

   Choose either or both of those options depending upon your intended user experience.
- If using alerts in the sidebar, include scenarios when an error state should appear so that badging can be used to alert users to take specific remedial actions.
- The app should be designed to pick the right events to show notifications or pop-out in a system browser, based on the desired use case. For example, consider which events should trigger the app to open (when the call first arrives, when the user answers it, etc.).

<a id="responsive-layout"></a>

### Responsive Layout

The app must be able to optimize its layout based on different viewports. From the Sidebar, the following scenarios apply: Maximized embedded view when the sidebar is collapsed; Smaller embedded view when the sidebar is expanded; Expanded view when the app is popped-out of the client in a resizable modal window

- [Pop-Out Window](https://developer.webex.com/docs/embedded-apps-design-and-experience-guidelines-for-sidebar#pop-out-window)
- [Sidebar-Collapsed](https://developer.webex.com/docs/embedded-apps-design-and-experience-guidelines-for-sidebar#sidebar-collapsed)
- [Sidebar-Expanded](https://developer.webex.com/docs/embedded-apps-design-and-experience-guidelines-for-sidebar#sidebar-expanded)
- [Scrolling Ability](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#scrolling-ability)

<a id="pop-out-window"></a>

### Pop-Out Window

The user can click the expand icon in the app's title bar to pop-out the app into a separate window at a default size of **788x552px**. Apps must be optimized for this default window size. Users can resize the pop-out window to any size, so apps must be responsive to other viewport sizes, including full screen.

![In-meeting default pop-out window size]( https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt75297eda841b8c6d/64497040d483864ab3657418/Pop-Out-Window.png)

<a id="sidebar-collapsed"></a>

### Sidebar Collapsed

![Sidebar-collapsed]( https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf7f4678d4477f51c/644970d41d4d37184e1ce891/Sidebar-Collapsed.png)

<a id="sidebar-expanded"></a>

### Sidebar Expanded

![Sidebar-expanded]( https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt75297eda841b8c6d/64497040d483864ab3657418/Pop-Out-Window.png)

<a id="scrolling-ability"></a>

### Scrolling Ability

Apps must provide users with the ability to easily scroll the app's visible content. 

<a id="platform-support"></a>

### Platform Support

Apps must be tested and verified to function as expected on all supported desktop systems including Windows and MacOS. Please note that Sidebar apps are not supported on Cisco Devices and Mobile devices at the moment.

<a id="use-of-pop-up-windows"></a>

### Use of Pop-up Windows

In general, apps should limit their use of pop-up windows created via JavaScript. In particular:

- Pop-up windows created via the `window.open()` JavaScript method must not be used for primary app workflows or experiences.

- Use of pop-ups must be limited to entering sign-in credentials, or displaying error messages or notification messages, only. Pop-up windows must be closed once the user has completed the sign-in process or acknowledged the notification or error message.

<a id="access-to-user-information"></a>

### Access to User Information

- Apps must not require a user to provide a phone number to enable use of the app. If the app solicits personal information from the user, it must not spam users with that information.
- Apps must not be dependent on access to a user's personally identifiable information (PII) to function properly. By default, access to PII in embedded apps is not enabled and apps must be able to function without access to PII. For more information, see [Access to Personally Identifying Information](https://developer.webex.com/docs/embedded-apps-guide#personally-identifiable-information-pii-and-embedded-apps).
- Embedded apps may obtain user information via an [Integration](https://developer.webex.com/docs/integrations) with [Webex APIs](https://developer.webex.com/docs/getting-started), but integrations should limit the [requested scopes](https://developer.webex.com/docs/integrations#scopes) to the minimum their application needs to function. For more information, see [Combined Webex Developer Solutions]() in the Embedded Apps Developer Guide. 

<a id="first-time-user-experience"></a>

### First-time User Experience

The following are requirements for the first-time user experience.

- Apps must be easy and intuitive for first-time users and provide clear call-to-actions (CTAs) in onboarding workflows.
- If a user is required to sign-in to use the app, all available sign-in methods in the app must be functional.
- If the user needs to first sign-up (create an external account) before using the app, the app must provide guidance on how users need to complete that process.

<a id="legibility-in-light-and-dark-modes"></a>

### Legibility in Light and Dark Modes

The Webex app provides users the option to enable dark or light mode for the user interface. All embedded app text and content must be visible, legible, and actionable in both color modes. In particular, apps must not have transparent backgrounds, which can make text illegible in dark mode.

<a id="other"></a>

### Other

- If an app encounters an error condition that it cannot recover from, it must provide users with graceful exit points and appropriate messaging about the error state.
- Apps that require a user to sign-in must also provide a way for the user to sign-out.
- Apps must not display advertisements. This requirement is evaluated on a per-app basis and depends on the situation (for example, if an app's underlying business model is dependent on ads).
- Apps must not include links to extraneous pages where not actionable (for example, links to "About", "Careers", or social media sites) that would leave the user "stranded".

## Recommended Design Guidelines

Embedded apps are expected to follow the recommended design guidelines discussed below. While not required for approval, apps that do not incorporate these recommended guidelines may not be approved for App Hub if the reviewer determines that the app provides a poor user experience.

Except where noted, the recommended design guidelines apply to both in-meeting, messaging and sidebar apps

- [Focus on Simplified Workflows and Use Cases](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#focus-on-simplified-workflows-and-use-cases)
- [Respond to User's Color Theme Preference](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#respond-to-user-s-color-theme-preference)
- [Sign-in Guidelines](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#sign-in-guidelines)

<a id="open-together-experience-recommendations"></a>

### Focus on Simplified Workflows and Use Cases

Developers should not try to repurpose or replicate their entire existing web app as an embedded app. Embedded apps benefit users with simplified use cases and workflows that add value to a Webex meeting or messaging space, or the sidebar of the Webex App. 

<a id="respond-to-user-s-color-theme-preference"></a>

### Respond to User's Color Theme Preference

Webex users can select a light or dark theme for the Webex or Meeting Center app. To provide the best user experience, embedded apps should be responsive to the user's theme preference and provide both light and dark color themes. Minimally, an app's light theme should provide dark-colored text on a light-colored background, while the dark theme should display light-colored text on a dark-colored background.

<a id="sign-in-guidelines"></a>

### Sign-in Guidelines

Apps that require user accounts should make the sign-up and sign-in processes as easy as possible for the user. Specifically, apps should incorporate the following:

- App recipients should have the same or similar sign-up and sign-in experience as the app initiator.
- Apps should use cookies and local storage to persist a user's log-in information, so that users do not need to log in each time they open a space tab or join an Open For All session. The embedded app version of your service or application should provide the same sign-in or session persistence as the browser-based version. See [Using Cookies and Web Storage](https://developer.webex.com/docs/embedded-apps-guide#cookies_local_storage) in the Embedded Apps developer guide for more information.
- Apps should use third-party identity providers for user sign-in only when necessary.

## Good-to-Have Design Guidelines

The following suggestions provide an enhanced user experience both within your app and in the larger Webex context. Incorporating these suggestions is optional and will not block app approval if not implemented.

### Provide a "Freemium" Model for First-time Users

Apps that require users to create an account and select a pricing plan should provide a "freemium" model to allow first-time users an easy sign-up experience. Apps can use the participant's [user ID](https://developer.webex.com/docs/embedded-apps-api-reference#type-definitions) to create a placeholder association between the user and the current app session. This ID is guaranteed to be unique regardless of whether the app has access to the user's personally identifiable information (PII).

### Accessibility Considerations

Apps should strive to be optimized for different types of users. For instance, an app should support logical keyboard navigation for users who cannot operate a mouse, as well as screen reader optimization and zoom support for visually impaired users. To learn more, refer to the W3C Accessibility Standards. This will ensure that as many users as possible have a seamless experience as they navigate between your app and Webex.
