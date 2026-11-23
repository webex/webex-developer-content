---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/browser
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Getting Started
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/browser). [Full Markdown](../../../../../docs/sdks/browser.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Limitations](007-limitations.md)

## Article introduction

Add Webex products and features to your web apps with the Webex Browser SDK.

[GitHub](<https://github.com/webex/webex-js-sdk>)
[NPM](<https://www.npmjs.com/package/webex>)

## Selected section

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
