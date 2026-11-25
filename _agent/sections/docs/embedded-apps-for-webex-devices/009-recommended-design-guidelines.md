---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-for-webex-devices
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Recommended Design Guidelines
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-for-webex-devices). [Full Markdown](../../../../docs/embedded-apps-for-webex-devices.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Technical Requirements and Limitations](007-technical-requirements-and-limitations.md) [Requirements for Embedded Apps on Devices](008-requirements-for-embedded-apps-on-devices.md)

## Selected section

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
