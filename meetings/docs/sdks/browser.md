---
type: Guide
title: Browser SDK
display_title: Browser
canonical_url: https://developer.webex.com/docs/sdks/browser
content_type: documentation
product_group:
- webex-suite
categories:
- calling
- meeting
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/browser)

Add Webex products and features to your web apps with the Webex Browser SDK.

[GitHub](<https://github.com/webex/webex-js-sdk>)
[NPM](<https://www.npmjs.com/package/webex>)

## Versions

- Current version: 3.7.0
- Previous major version: 3.3.0

The `next` branch of the SDK contains the latest features and fixes. Use the last published tag from the [tags](https://github.com/webex/webex-js-sdk/tags) page to find the release you'd like to consume.

## Features

- Create and join audio and/or video meetings
- Create by email address, or SIP address. (Note: SIP URIs are only supported for cloud-registered Webex devices, not third-party SIP endpoints or Webex Calling.)
- Meeting and event controls
- Audio and video meeting control
- Maximum bandwidth controls
- View shared content
- Share screen/application from desktop browsers: Chrome, Firefox, Edge (80+), and Safari (12.1+)
- Device Controls (get device list, send PIN, pair)
- Device Search
- Personal Meeting Room support
- Move Media
- Moderator Controls
- Reception of Real-Time Transcripts. (Note: Real-Time Transcription is ONLY supported by meetings where Webex Assistant can be enabled, which requires a paid license.)
- FedRAMP environment support. See [usage README](https://github.com/webex/webex-js-sdk#fedramp-environment)
- [Background Noise Reduction](https://github.com/webex/webex-js-sdk/wiki/Background-Noise-Reduction)
- [Full HD Support](https://github.com/webex/webex-js-sdk/wiki/Video-Resolution)
- [TLS 443 Support](https://github.com/webex/webex-js-sdk/wiki/TLS-443-Support) New

## Getting Started

In this guide, we'll create a Node.js project with the Browser SDK and make a Webex meeting.



> **Info**
>
> To more easily follow along with this guide, the codebase is available on GitHub: [https://github.com/WebexSamples/webex-meetings-quick-start](https://github.com/WebexSamples/webex-meetings-quick-start)



### Requirements

- [Node.js](https://nodejs.org/) LTS 16.x and later, [npm](https://www.npmjs.com/) 6.x and later
- Optionally: [nvm](https://github.com/creationix/nvm/) to manage Node.js versions
- Supported Desktop Browsers: Chrome (latest), Firefox (latest), Edge (latest), and Safari (latest)
- Supported Mobile Browsers: Chrome for Android (latest) and Safari for iOS (latest)

### Step 1: Create the New Project

Create the project directory and change directories into it, as shown below:

```bash
mkdir webex-meetings
cd webex-meetings
```

### Step 2: Create HTML for the App

For this app, we'll create a very simple HTML file to load the SDK, provide a form to specify the meeting destination, and buttons to join and hangup.
We'll wire up this form in JavaScript to create and join a meeting!

Create a file called `index.html` in the root of the project directory with the following contents:

```html
<!DOCTYPE html>
<html>
  <title>Webex Meetings Quick Start</title>
  <body>
    <h1>Meetings Quick Start</h1>
    <p>This sample demonstrates how to start a meeting using Webex JS-SDK in the browser.</p>

    <form id="destination">
      <input
        id="invitee"
        name="invitee"
        placeholder="Person ID or Email Address or SIP URI or Room ID"
        type="text"
       />
        <input title="join" type="submit" value="join" />
    </form>

    <div style="display: flex">
      <video style="width:50%" id="self-view" muted autoplay></video>
      <div style="width:50%">
        <audio id="remote-view-audio" autoplay></audio>
        <video id="remote-view-video" autoplay></video>
      </div>
    </div>

    <button id="hangup" title="hangup" type="button">cancel/hangup</button>

    <script crossorigin src="https://unpkg.com/webex@3.7.0/umd/webex.min.js"></script>
    <script src="./index.js"></script>
  </body>
</html>
```

### Step 3: Access the JavaScript SDK

A UMD bundle version of the SDK is available on [unpkg](https://unpkg.com/). All we have to do is add a `<script>` tag in our `index.html` that points to it.
Looking at the code in step 2, we've already done so with the line:

```html
<script crossorigin src="https://unpkg.com/webex@3.7.0/umd/webex.min.js"></script>
```

New versions of the JavaScript SDK are released frequently, using `@3.7.0` as the version will give you access to the latest version of the JavaScript SDK while avoiding major breaking changes.



> **Info**
>
> The following CDN URL is available as a backup: `https://cdn.jsdelivr.net/npm/webex@3.7.0/umd/webex.min.js`.



The code for our app will be loaded in our `index.html` file with `<script src="./index.js"></script>`. We'll create this file in the next step.

Notice that the `<script>` tag for the SDK bundle must come before our `index.js`, otherwise the contents of the SDK will not be available to our `index.js` script.

### Step 4: Authenticate App with Webex

For this example, we'll use your personal access token which can be found in [Getting Started](https://developer.webex.com/docs/api/getting-started#accounts-and-authentication) if you're logged in.

This token provides access to your account for testing purposes, and shouldn't be used for anything other than testing. If you don't already have a Webex account, click Sign Up at the top of this page to create a new account.

#### Authenticate with Webex

Create the `index.js` file and add this code to authenticate with Webex, replacing `YOUR_ACCESS_TOKEN` with your development token:

```javascript
// index.js
const webex = window.Webex.init({
  credentials: {
    access_token: `YOUR_ACCESS_TOKEN`
  }
});
```

### Step 5: Add Meeting Capabilities to our JavaScript

All of the meeting functionality for this app will live in our app's main JavaScript file, `index.js`.

#### Register with Webex Cloud

We'll need to register and connect with the Webex Cloud before attempting to join a meeting. Add the following code to your `index.js` file:

```javascript
webex.meetings.register()
  .catch((err) => {
    console.error(err);
    alert(err);
    throw err;
  });
```

#### Set up Event Listeners for Meeting Events

When we make a meeting, the SDK will generate several events to keep us informed about the meeting's progress such as media stream changes, hangups, etc. Let's watch for these events by adding this code:

```javascript
function bindMeetingEvents(meeting) {
  meeting.on('error', (err) => {
    console.error(err);
  });

  // Handle media streams changes to ready state
  meeting.on('media:ready', (media) => {
    if (!media) {
      return;
    }
    if (media.type === 'remoteVideo') {
      document.getElementById('remote-view-video').srcObject = media.stream;
    }
    if (media.type === 'remoteAudio') {
      document.getElementById('remote-view-audio').srcObject = media.stream;
    }
  });

  // Handle media streams stopping
  meeting.on('media:stopped', (media) => {
    // Remove media streams
    if (media.type === 'remoteVideo') {
      document.getElementById('remote-view-video').srcObject = null;
    }
    if (media.type === 'remoteAudio') {
      document.getElementById('remote-view-audio').srcObject = null;
    }
  });

  // Of course, we'd also like to be able to leave the meeting:
  document.getElementById('hangup').addEventListener('click', () => {
    meeting.leave();
  });
}
```

#### Set up Join Meeting handler

When our meeting is created, we are not automatically joined into it. Let's create a helper function that will join the meeting for us.

```javascript
// Join the meeting and add media through joinWithMedia method.
async function joinMeeting(meeting) {

    const microphoneStream = await webex.meetings.mediaHelpers.createMicrophoneStream({
      echoCancellation: true,
      noiseSuppression: true,
    });

    const cameraStream = await webex.meetings.mediaHelpers.createCameraStream({ width: 640, height: 480 });
    document.getElementById('self-view').srcObject=cameraStream.outputStream;

    const meetingOptions = {
      mediaOptions: {
        allowMediaInLobby: true,
        shareAudioEnabled: false,
        shareVideoEnabled: false,
        localStreams:{
          camera:cameraStream,
          microphone: microphoneStream
        },      
      },
    };

    await meeting.joinWithMedia(meetingOptions);

  } 
```

#### Set up Event Listener for the Join Button

In our simple HTML page, we added a form with a few buttons to start and end the meeting. Let's add an event listener to initiate the meeting when the `join` button is clicked:

```javascript
document.getElementById('destination').addEventListener('submit', (event) => {
  // again, we don't want to reload when we try to join
  event.preventDefault();

  const destination = document.getElementById('invitee').value;

  return webex.meetings.create(destination).then((meeting) => {
    // Call our helper function for binding events to meetings
    bindMeetingEvents(meeting);

    return joinMeeting(meeting);
  })
  .catch((error) => {
    // Report the error
    console.error(error);
  });
});
```
Now, when we click `join`, we'll use the SDK's `meetings.create` and `meeting.joinWithMedia` methods to create and join the meeting.

#### Final index.js file

Your `index.js` file should look like this when completed:

```javascript
const myAccessToken = 'YOUR_ACCESS_TOKEN';

if (myAccessToken === 'YOUR_ACCESS_TOKEN') {
  alert('Make sure to update your access token in the index.js file!');
  return;
}

const webex = window.Webex.init({
  credentials: {
    access_token: myAccessToken
  }
});

webex.meetings.register()
  .catch((err) => {
    console.error(err);
    alert(err);
    throw err;
  });

function bindMeetingEvents(meeting) {
  meeting.on('error', (err) => {
    console.error(err);
  });

  // Handle media streams changes to ready state
  meeting.on('media:ready', (media) => {
    if (!media) {
      return;
    }
    if (media.type === 'remoteVideo') {
      document.getElementById('remote-view-video').srcObject = media.stream;
    }
    if (media.type === 'remoteAudio') {
      document.getElementById('remote-view-audio').srcObject = media.stream;
    }
  });

  // Handle media streams stopping
  meeting.on('media:stopped', (media) => {
    // Remove media streams
    if (media.type === 'remoteVideo') {
      document.getElementById('remote-view-video').srcObject = null;
    }
    if (media.type === 'remoteAudio') {
      document.getElementById('remote-view-audio').srcObject = null;
    }
  });

  // Of course, we'd also like to be able to leave the meeting:
  document.getElementById('hangup').addEventListener('click', () => {
    meeting.leave();
  });
}

// Join the meeting and add media through joinWithMedia method.
async function joinMeeting(meeting) {

    const microphoneStream = await webex.meetings.mediaHelpers.createMicrophoneStream({
      echoCancellation: true,
      noiseSuppression: true,
    });

    const cameraStream = await webex.meetings.mediaHelpers.createCameraStream({ width: 640, height: 480 });
    document.getElementById('self-view').srcObject=cameraStream.outputStream;

    const meetingOptions = {
      mediaOptions: {
        allowMediaInLobby: true,
        shareAudioEnabled: false,
        shareVideoEnabled: false,
        localStreams:{
          camera:cameraStream,
          microphone: microphoneStream
        },      
      },
    };

    await meeting.joinWithMedia(meetingOptions);

  } 

document.getElementById('destination').addEventListener('submit', (event) => {
  // again, we don't want to reload when we try to join
  event.preventDefault();

  const destination = document.getElementById('invitee').value;

  return webex.meetings.create(destination).then((meeting) => {
    // Call our helper function for binding events to meetings
    bindMeetingEvents(meeting);

    return joinMeeting(meeting);
  })
  .catch((error) => {
    // Report the error
    console.error(error);
  });
});
```

### Step 6: Load the Web App

Let's serve the web app with a [simple HTTP server](https://www.npmjs.com/package/http-server) and start a meeting in the browser!

```bash
npx http-server ./ -p 1234
```

Open the app ([http://localhost:1234](http://localhost:1234/)) in your browser to use your new web app!
Enter the Person ID or email address of who you want to start a meeting with and click the `start meeting` button.
Congratulations, you've made your first meeting in the browser using the Webex Browser SDK! 🎉



> **Info**
>
> Most browsers require an HTTPS connection to access certain browser features such as cameras and microphones. To use HTTPS while developing your application, see [using http-server with TLS/SSL](https://www.npmjs.com/package/http-server#tlsssl). Ensure that your production application is deployed using HTTPS.



## Live Demo and Sample Code

To help you get up and running quickly, we've created a live demo, along with its corresponding sample code as well!

[Browser SDK Live Demo](<https://webex.github.io/webex-js-sdk/samples/browser-plugin-meetings/>)

[Browser SDK Demo Sample Code](<https://github.com/webex/webex-js-sdk/tree/next/docs/samples/browser-plugin-meetings>)

## SDK API Reference

In-depth API reference information for the Browser SDK API can be found here:

https://webex.github.io/webex-js-sdk/api/

## Upgrading

The `plugin-phone` plugin is deprecated and replaced with `plugin-meetings`. With this change comes significant code changes in upgrading to the meetings plugin. The meetings plugin is much more feature rich and maintained than the phone plugin.

For users of the phone plugin, one of the main changes from plugin-phone is the idea of having a meeting object that we are performing actions on. Instead of just "calling" a destination, a meeting object must be "created" and then "joined".

For more detailed information, please see the [upgrade guide](https://github.com/webex/webex-js-sdk/blob/master/packages/node_modules/%40webex/plugin-meetings/UPGRADING.md)

## Limitations

- Sharing from iOS and Android browsers is currently not supported due to OS limitations

## Support Policy

Please visit the [Webex API and SDK Support Policy](https://developer.webex.com/docs/webex-api-and-sdk-support-policy) page for details on our support and end of life policy for APIs and SDKs.

## Troubleshooting

If you're having trouble with the Browser SDK, here's some more information to help troubleshoot the issue.

### SDK Requirements

Review the following SDK requirements to make sure you're using the correct minimum versions of Node.js, npm, etc.:

- [Node.js](https://nodejs.org/) LTS 16.x and later
- [npm](https://www.npmjs.com/) 6.x and later
- Optionally: [nvm](https://github.com/creationix/nvm/) to manage Node.js versions
- Supported Desktop Browsers: Chrome (latest), Firefox (latest), and Safari (latest)
- Supported Mobile Browsers: Chrome for Android and Safari for iOS
- A Webex account and an integration with the necessary [scopes](https://developer.webex.com/docs/integrations#scopes)

**Note:**

- If you are joining a meeting with a browser on an Android 12 device (Pixel or other Android devices, except Samsung), the remote video could be corrupted. This issue is fixed in Google Chrome v97 (https://chromereleases.googleblog.com/). Please upgrade to this version.
- If you are using the BrowserSDK to join a meeting with Safari on an iPhone with iOS 15.1, you may experience an issue after calling `addMedia()` to join the meeting. This has been traced to a [known webRTC bug](https://bugs.webkit.org/show_bug.cgi?id=232490) with Safari on iOS 15.1. This issue has been fixed in iOS 15.2, so upgrading to 15.2 should fix the issue.

### Additional Logging

You can add additional logging to your application to help narrow down any issues with the SDK.

#### Change the Log Level Within Your App

When you initialize the JavaScript SDK, you can set the log level to `info` to see more logging to help troubleshoot the issue:

```javascript
const webex = window.Webex.init({
  credentials: {
    access_token: myAccessToken
  },
  logger: {
    level: 'info'
  }
});

```

To see even more logging, set the log level to `debug`.

### Firewall Ports

The Browser SDK makes use of several network protocols and ports. If you're encountering connection or connectivity issues, make sure there aren't any firewalls blocking or preventing communication with any Webex endpoints. For more information about the network and web security requirements for Webex services, please see [Network Requirements for Webex Services](https://help.webex.com/WBX000028782/).

### Getting Support

If you're stumped, contact the [Webex Developer Support team](https://developer.webex.com/support) for more help with the SDK.
