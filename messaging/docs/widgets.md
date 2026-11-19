---
type: Guide
title: Widgets
display_title: Widgets
canonical_url: https://developer.webex.com/docs/widgets
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/widgets)

Embed the power of Webex in your web applications ✨

## Widgets Overview

Webex Widgets provide Webex native application functionality that can be embedded into any web-based application.
They are built with [React](https://reactjs.org/), [Redux](https://redux.js.org/), [RxJS](https://rxjs.dev/) and the [Browser SDK](https://developer.webex.com/docs/sdks/browser) to communicate with the Webex Platform.

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltdacf41cab87b09ea/61b38354aeb5451282be2869/Widgets-Example.png" width="100%" title="Widget example in Salesforce" />

Widgets can be embedded directly in web applications with few lines of code, giving incredible flexibility to many different collaboration workflows without missing out on the Webex features we all love.
Widgets come pre-built with the Webex User Interface (UI).

They can be used by either current Webex users or guests by authenticating with an auth token provided from an [integration](https://developer.webex.com/docs/integrations) or a [guest issuer](https://developer.webex.com/docs/guest-issuer) app.

Today there are three different embeddable experiences available: [Space Widget](https://developer.webex.com/docs/widgets#space-widget), [Recents Widget](https://developer.webex.com/docs/widgets#recents-widget), and [Meetings Widget](https://developer.webex.com/docs/widgets#meetings-widget-).

## Space Widget

Include Webex space functionality in your app.
This widget provides messaging, meeting and content sharing features related to spaces.
Join 1:1 or group spaces to collaborate via messaging or start and join meetings, all with the familiar Webex UI.

[GitHub](<https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-space#webex-space-widget-webexwidget-space>)
[Demo App](<https://code.s4d.io/widget-demo/production/index.html>)

### Space Widget Features



  <ul>
    <li>
      Messaging:
      <ul>
        <li>1:1 and group messaging</li>
        <li>Markdown message support</li>
        <li>File sharing. (150MB file size limit)</li>
        <li>Delete/flag messages</li>
        <li>Read receipts</li>
        <li>Persistent chat</li>
        <li>Roster list and @mention</li>
      </ul>
    </li>
    <li>
      Meetings:
      <ul>
        <li>Join 1:1/Group Space meetings using password or hostkey based authentication</li>
        <li>Dial by email address or SIP address.
          <i><b>Note:</b> SIP addresses are only supported for Webex meetings SIP URIs and not for Webex Calling or 3rd party SIP URIs</i></li>
        <li>Share screen or a specific application/browser tab. Note: Safari browsers ONLY support sharing the whole screen</li>
      </ul>
    </li>
    <li>FedRAMP environment support. See the <a href="https://github.com/webex/widgets#fedramp-environment">usage README</a>.</li>
  </ul>


  <img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8d57b2446b4648ca/61b383539a45fb1280c1938d/Space-Widget-Messaging.png" title='Messaging on Space Widget' width="100%" />



### Space Widget Usage

To use this widget, you'll first need to create an [integration](https://developer.webex.com/docs/integrations) with the following scopes: `spark:all`.

Using our CDN requires the least amount of work to get started. Add the following to your HTML file:

```html
<!-- Latest compiled and minified CSS -->
<link rel="stylesheet" href="https://code.s4d.io/widget-space/production/main.css">

<!-- Latest compiled and minified JavaScript -->
<script src="https://code.s4d.io/widget-space/production/bundle.js"></script>
```

You can then instantiate the widget by providing an `ACCESS_TOKEN` and `SPACE_ID`:

```html
<div id="my-space-widget" />

<script>
  // Grab DOM element where widget will be attached
  var widgetEl = document.getElementById('my-space-widget');

  // Initialize a new Space widget
  webex.widget(widgetEl).spaceWidget({
    accessToken: 'ACCESS_TOKEN',
    destinationType: 'spaceId',
    destinationId: 'SPACE_ID'
  });
</script>
```

If you'd like to use a guest token instead of an access token, use the `guestToken` parameter with a guest token instead of `accessToken`.

For more usage and configuration information, see the [Space Widget Usage](https://github.com/webex/react-widgets/blob/master/packages/node_modules/%40webex/widget-space/README.md#usage) documentation in GitHub.

### Space Widget Requirements

Supported Desktop Browsers: Chrome (latest), Firefox (latest), and Safari (latest).

Please note that Space Widget _is not supported on Mobile browsers_.

## Recents Widget

Include a user's most recent Webex spaces in your app and respond to real-time events.
This widget displays a list of recent Webex spaces and can act as a central event processing hub for events happening within the Webex Platform.

[GitHub](<https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-recents#webex-recents-widget-webexwidget-recents>)
[Demo App](<https://code.s4d.io/widget-demo/production/index.html>)

### Recents Widget Features



  <ul>
    <li>Recent Webex conversation list (spaces & people)</li>
    <li>Hooks to open a conversation with the Space Widget</li>
    <li>Unread space highlighting</li>
    <li>Event hooks for messages, meetings, and memberships</li>
    <li>Incoming call notifications</li>
    <li>FedRAMP environment support. See the <a href="https://github.com/webex/widgets#fedramp-environment">usage README</a>.</li>
  </ul>


  <img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf7f2462ef3ae82f5/61b38353a342a6586354334d/Recents.png" title="Recents widget" width="100%" />



### Recents Widget Usage

To use this widget, you'll first need to create an [integration](https://developer.webex.com/docs/integrations) with the following scopes: `spark:all`.

Using our CDN requires the least amount of work to get started. Add the following to your HTML file:

```html
<!-- Production compiled and minified CSS -->
<link rel="stylesheet" href="https://code.s4d.io/widget-recents/production/main.css">

<!-- Production compiled and minified JavaScript -->
<script src="https://code.s4d.io/widget-recents/production/bundle.js"></script>
```

You can then instantiate the widget by providing an `ACCESS_TOKEN`:

```html
<div id="my-recents-widget" />

<script>
  // Grab DOM element where widget will be attached
  var widgetEl = document.getElementById('my-recents-widget');

  // Initialize a new Recents widget
  webex.widget(widgetEl).recentsWidget({
    accessToken: 'ACCESS_TOKEN'
  });
</script>
```

If you'd like to use a guest token instead of an access token, use the `guestToken` parameter with a guest token instead of `accessToken`.

For more usage and configuration information, see the [Recents Widget Usage](https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-recents#usage) documentation in GitHub.

### Recents Widget Events

The Recents Widget exposes a few events for hooking into widget functionality.
When instantiating a Recents widget, you can provide a callback parameter that will fire whenever an event occurs.
You can then filter the actions and perform actions:

```html
<div id="my-recents-widget" />

<script>
  // Grab DOM element where widget will be attached
  var widgetEl = document.getElementById('my-recents-widget');

  // Initialize a new Recents widget
  webex.widget(widgetEl).recentsWidget({
    accessToken: 'ACCESS_TOKEN',
    onEvent: callback
  });

  function callback(name, detail) {
    if (name === 'messages:created') {
      // Perform an action if a new message has been created
    }
  }
</script>
```

See the [Recents Widget Events](https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-recents#events) documentation in GitHub for more information about event handling.

### Recents Widget Requirements

Supported Desktop Browsers: Chrome (latest), Firefox (latest), and Safari (latest)

Please note the Recents Widget _is not supported on Mobile browsers_.

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

## Content Security Policy

Webex Widgets can be used on websites which implement a Content Security Policy (CSP) via the Content-Security-Policy HTTP header.
Consult your webserver's documentation for more information about configuring CSP.
If you're using CSP, use these individual policy directives and their associated values to enable access to the widgets and to allow connectivity to the Webex Platform:

| Policy Directive| Value |
| --- | --- |
| `script-src` | `'self' 'unsafe-inline' https://code.s4d.io;` |
| `style-src` | `'self' 'unsafe-inline' https://code.s4d.io;` |
| `media-src` | `'self' https://code.s4d.io https://*.clouddrive.com https://*.giphy.com https://*.webexcontent.com data: blob:;` |
| `font-src` | `'self' https://code.s4d.io;` |
| `img-src` | `'self' https://*.clouddrive.com https://code.s4d.io https://*.webexcontent.com data: blob: https://*.rackcdn.com;` |
| `connect-src` | `'self' localhost ws://localhost:8000 wss://*.ciscospark.com wss://*.wbx.com wss://*.wbx2.com https://*.ciscospark.com https://*.clouddrive.com/ https://code.s4d.io https://*.giphy.com https://*.wbx2.com https://*.webex.com  https://*.webexcontent.com;` |

## Support Policy

For information on the Webex support policy, see the [SDK and API Support Policy](https://developer.webex.com/docs/api-and-sdk-support-policy).
