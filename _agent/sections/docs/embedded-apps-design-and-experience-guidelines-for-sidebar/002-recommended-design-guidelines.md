---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-design-and-experience-guidelines-for-sidebar
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Recommended Design Guidelines
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-design-and-experience-guidelines-for-sidebar). [Full Markdown](../../../../docs/embedded-apps-design-and-experience-guidelines-for-sidebar.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements for Sidebar Embedded Apps](001-requirements-for-sidebar-embedded-apps.md)

## Article introduction

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

## Selected section

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
