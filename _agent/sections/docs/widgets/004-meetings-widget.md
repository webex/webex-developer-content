---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Meetings Widget 🆕
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets). [Full Markdown](../../../../docs/widgets.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Embed the power of Webex in your web applications ✨

## Selected section

## Meetings Widget 🆕

Include [Webex Meetings](https://www.webex.com/video-conferencing) functionality into your application to join any Webex meeting type, share your screen, manage your media devices and more.
The Meetings Widget comes in two themes: Dark and Light and is designed to be responsive, which gives you maximum flexibility on where it can be used!

[GitHub](<https://github.com/webex/widgets#webex-widgets>)
[Demo App](<https://webex.github.io/widgets/>)

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5aadc1c793ca9332/6192730a3b08dd14d79a8984/meetings-widget.png"  title='Meetings Widget in Light theme' />

### Meetings Widget Features

#### Meetings

* Join 1:1 or group Space meetings, Personal Meeting Rooms and Scheduled meetings with password or hostkey based authentication.
* Dial by email address, people ID, room ID or SIP address
_**Note:** SIP addresses are supported for Webex meetings SIP URIs and Webex cloud-registered devices. Webex Calling or third-party SIP URIs are not supported_
* In-meeting participant roster. See participants from your organization and those from outside
* Share your screen or a specific application/browser tab
_**Note:** Screen sharing is a desktop-browser-only feature (See [compatibility table](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getDisplayMedia#browser_compatibility)). MacOS Safari only supports sharing the whole screen_
* FedRAMP environment support. See the [usage README](https://github.com/webex/widgets#fedramp-environment).

#### Media Management

* List available audio/video devices
* Mute/Unmute your audio/video before joining and during the meeting
* Switch your audio/video device before joining and during the meeting

#### Customization

* Choose between the amazing Dark or Light Webex experiences
* Show/hide meeting controls (mute, settings, participants list, screen share, etc.) based on your use case
* Decide which remote video layout (e.g. grid, stack, focus) is best for your application

#### Accessibility

* Screen-reader ready
* Keyboard navigation

### Widget Usage

Meetings Widget is [available on NPM](https://www.npmjs.com/package/@webex/widgets) with no support of distribution via CDN at the moment.

To get started with the Meetings widget, install [the widget package](https://www.npmjs.com/package/@webex/widgets) and its dependencies.



> **Info**
>
> Note: Widgets is only supported on **Node.js v20** and below.

<br>

```bash
npx install-peerdeps @webex/widgets
```

Import widget package and styles, instantiate a new widget by providing an `ACCESS_TOKEN` and a `MEETING_DESTINATION`:

```javascript
import {WebexMeetingsWidget} from '@webex/widgets';

import '@webex/widgets/dist/css/webex-widgets.css';

export default function App() {
  return (
    <WebexMeetingsWidget
      style={{width: "1000px", height: "500px"}} // Substitute with any arbitrary size or use `className`
      accessToken="<ACCESS_TOKEN>"
      meetingDestination="<MEETING_DESTINATION>"
    />
  );
}

```

See [Accounts and Authentication](https://developer.webex.com/docs/getting-started#accounts-and-authentication) on how to obtain an access token. For production use, you will need to create an [integration](https://developer.webex.com/docs/integrations) with the following scopes: `spark:all`.

At the moment, guest tokens are not supported directly, but you may use the access token provided after [guest token exchange flow](https://developer.webex.com/docs/guest-issuer#using-guest-tokens).

You can also get started with our [Meetings widget sample repository](https://github.com/WebexSamples/webex-meeting-widget-starter).

### Meetings Widget Requirements

* Supported Desktop Browsers: Chrome (latest), Firefox (latest), Edge (latest) and Safari (latest)
* Supported Mobile Browsers: Chrome on Android (latest) and Safari on iOS (latest)

Meetings widget general availability support starts on version 1.23.0 onwards.
However, we encourage you to use use the latest version at the time and update regularly, as there will be tons of improvements and bug fixes!
