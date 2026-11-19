---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Recommended Design Guidelines
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces). [Full Markdown](../../../../docs/embedded-apps-design-guidelines-for-spaces.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements for In-Space Embedded Apps](001-requirements-for-in-space-embedded-apps.md)

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

## Recommended Design Guidelines

Embedded apps are expected to follow the recommended design guidelines discussed below. While not required for approval, apps that do not incorporate these recommended guidelines may not be approved for App Hub if the reviewer determines that the app provides a poor user experience.

* [Focus on Simplified Workflows and Use Cases](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces#focus-on-simplified-workflows-and-use-cases)
* [Respond to User's Color Theme Preference](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces#respond-to-user-s-color-theme-preference)
* [Tab Names for In-Space Apps](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces#tab-names-for-in-space-apps)
* [Sign-in Guidelines](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces#sign-in-guidelines)

<a id="focus-on-simplified-workflows-and-use-cases"></a>

### Focus on Simplified Workflows and Use Cases

Developers should not try to repurpose or replicate their entire existing web app as an embedded app. Embedded apps benefit users with simplified use cases and workflows that add value to a Webex meeting or messaging space.

<a id="respond-to-user-s-color-theme-preference"></a>

### Respond to User's Color Theme Preference

Webex users can select a light or dark theme for the Webex app. To provide the best user experience, embedded apps should be responsive to the user's theme preference and provide both light and dark color themes. Minimally, an app's light theme should provide dark-colored text on a light-colored background, while the dark them should display light-colored text on a dark-colored background.

![Slido app adpating to light and dark color themes in Webex app](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2b8331f339dbb0b6/61b90cc5c52c5b292ce22f36/slido-light-dark.png)

<a id="tab-names-for-in-space-apps"></a>

### Tab Names for In-Space Apps

Each space tab is assigned a name (via the [setShareURL()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+setShareUrl) method) that appears on each tab. For example, the following image shows a tab named "Brainstorming."

![Simple tab name without app name](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte082a79c73814008/61b9198c130d60617080267f/tab-name-short.png)

To help users quickly identify tab names with a minimum number of visible characters, it is recommended that tab names **not** be prefixed with the app name. For example, the following demonstrates an example of this anti-pattern where the tab name includes the name of the app, "White Board," in this example.

![Anti-pattern of tab name with app name](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3819db8f5f6812b2/61b9198cd73c783f9a3d1616/tab-name-long.png)

<a id="sign-in-guidelines"></a>
### Sign-in Guidelines

Apps that require user accounts should make the sign-up and sign-in processes as easy as possible for the user. Specifically, apps should incorporate the following:

* App recipients should have the same or similar sign-up and sign-in experience as the app initiator.
* Apps should use cookies and local storage to persist a user's log-in information, so that users do not need to log in each time they open a space tab. The embedded app version of your service or application should provide the same sign-in or session persistence as the browser-based version. See [Using Cookies and Web Storage](https://developer.webex.com/docs/embedded-apps-guide#cookies_local_storage) in the Embedded Apps developer guide for more information.
* Apps should use third-party identity providers for user sign-in only when necessary.
