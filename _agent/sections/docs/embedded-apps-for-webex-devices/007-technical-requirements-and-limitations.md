---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-for-webex-devices
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Technical Requirements and Limitations
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-for-webex-devices). [Full Markdown](../../../../docs/embedded-apps-for-webex-devices.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements for Embedded Apps on Devices](008-requirements-for-embedded-apps-on-devices.md)

## Selected section

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
