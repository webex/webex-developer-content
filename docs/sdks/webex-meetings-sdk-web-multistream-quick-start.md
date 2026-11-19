---
type: Guide
title: Web Meetings SDK | Multistream Quickstart
display_title: Multistream Quickstart
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-multistream-quick-start
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-multistream-quick-start)

With multistream, developers gain greater flexibility when displaying remote media streams. Instead of receiving a single stream featuring all participants, multistream enables the showcasing of multiple streams simultaneously. This means you can easily view each remote participant's stream individually, enhancing clarity and engagement during collaborative sessions.

---

This guide provides a quick glimpse into consuming multistream in Webex Meetings using the Webex JavaScript SDK. You'll find code snippets below that can quickly get you up and running.

## Initialize the SDK

To work with the multistream feature you'll need to install via npm or yarn or reference via an HTML `<script>` tag, the Meetings Web SDK version 3.1.0 or higher:

### NPM

```bash
npm install webex
```

### Yarn

```bash
yarn add webex
```

### HTML

```html
<script defer src="https://unpkg.com/webex@3.7.0/umd/webex.min.js"></script>
```

## Enable Multistream

To integrate multistream functionality into your meetings, include the `enableMultistream` flag within the `joinOptions` parameter when calling either the `meeting.join()` or `meeting.joinWithMedia()` methods:

```js
const joinOptions = {
  enableMultistream: true,
  ...
};

// Use either the join() method:

await meeting.join(joinOptions);

// ...or the joinWithMedia() method:

await meeting.joinWithMedia({joinOptions, mediaOptions});
```



> **Info**
>
> For additional details, see [Join a Meeting](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-join-a-meeting).



## Build the Layout

The layout determines how the various streams are positioned and displayed in the user interface. In order to create the layout with remote streams:

1. Create HTML container elements (for example a `<div>`) for the video streams:

    ```html
    <div id="multistream-remote-video" style="display: flex">
      <!-- All the remote videos will render here -->
    </div>
    ```

1. For each streams
    1. Create an HTML `<video>` element and attach the `remoteMedia.stream`.

        ```js
        // Create an html "video" element and attach the `remoteMedia.stream`
        function createVideoElement(stream) {
          const videoElement = document.createElement('video');
          videoElement.srcObject = stream;
          videoElement.height = 480;
          videoElement.width = 620;
          videoElement.autoplay = true;
          videoElement.muted = true;

          return videoElement;
        }
        ```

    1. **(Optional)** Add elements for name label, overlay and overlay text elements to display participant information on top of the video streams.
1. Append all the video elements to the container element.

    ```js
    const remoteVideoContainerElm = document.getElementById('multistream-remote-video');
    
    function updateTheLayout(activeSpeakerVideoElems, memberVideoElems) {
      [...activeSpeakerVideoElems, ...memberVideoElems].forEach((videoElement) => {
        // Append all the video elements to the container element
        remoteVideoContainerElm.appendChild(videoElement);
      });
    }
    ```

## Setup Remote Media Event Listeners

Once you've joined a meeting successfully, the meetings backend will start sending the remote streams which can be received by listening to the following two events:



> **Info**
>
> When multistream is enabled, media cannot be accessed or listened to on the `media:ready` event. Instead, you should listen to the media events received during a meeting that pertain to multistream, such as `media:remoteVideo:layoutChanged`, to handle media streams appropriately.



- `media:remoteAudio:created` - For remote audio streams.
- `media:remoteVideo:layoutChanged` - For remote video streams including active speaker, participants and screen sharing.

### Attach Audio Streams

You'll need to define HTML elements to which you'll attach the audio streams. For example:

```html
<!-- Audio elements -->
<audio id="multistream-remote-audio-0" class="multistream-remote-audio" autoplay></audio>
<audio id="multistream-remote-audio-1" class="multistream-remote-audio" autoplay></audio>
<audio id="multistream-remote-audio-2" class="multistream-remote-audio" autoplay></audio>
```



> **Info**
>
> You can only receive a maximum of 3 audio streams from active speakers at a time.



To bind the streams to the HTML elements, you can use the following JavaScript snippet:

```js
meeting.on('media:remoteAudio:created', (audioMediaGroup) => {
  audioMediaGroup.getRemoteMedia().forEach((media, index) => {
    document.getElementsByClassName('multistream-remote-audio')[index].srcObject = media.stream;
  });
});
```

### Attach Video Streams

Now, let's link all the remote video and screenshare streams here by listening for the `media:remoteVideo:layoutChanged` event and updating the video elements accordingly:

```js
const remoteScreenshareElm = document.getElementById('remote-screenshare');

const activeSpeakerVideoElems = [];
const memberVideoElems = [];

meeting.on('media:remoteVideo:layoutChanged', ({
  layoutId, activeSpeakerVideoPanes, memberVideoPanes, screenShareVideo
}) => {
  for (const [groupId, group] of Object.entries(activeSpeakerVideoPanes)) {
    group.getRemoteMedia().forEach((remoteMedia, index) => {
      // Attach the "remoteMedia.stream" of active speakers to video elements
      if(remoteMedia.sourceState === 'live') {
        activeSpeakerVideoElems.push(createVideoElement(remoteMedia.stream));
      }
    });
  }

  // The Staged layout has memberVideoPanes defined. Read through the comprehensive guide for more details.
  for (const [paneId, remoteMedia] of Object.entries(memberVideoPanes)) {
    // Attach the "remoteMedia.stream" of member videos to video elements
    if(remoteMedia.sourceState === 'live') {
      memberVideoElems.push(createVideoElement(remoteMedia.stream));
    }
  }

  updateTheLayout(activeSpeakerVideoElems, memberVideoElems);

  if (screenShareVideo) {
    // Attach the "screenShareVideo.stream" to a video element
    remoteScreenshareElm.srcObject = screenShareVideo.stream;
  }
});
```

Now that you've witnessed multistream in action, for a more thorough understanding and access to all available features, see the [Multistream Comprehensive Guide](https://github.com/webex/webex-js-sdk/wiki/Multistream-Comprehensive-Guide).

## Kitchen Sink App

To experiment with more features of multistream, see the [Meeting Samples App](https://webex.github.io/webex-js-sdk/samples/browser-plugin-meetings/).

When using the sample app, in the **Manage Meeting** section, select the checkbox labeled **Use a multistream connection** (which automatically sets `enableMultistream` to true and passes it to the `join()` methods) before clicking on `Join Meeting` or `Join with Media`:

![Enable multistream in the sample app](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc9074d83e5609144/enableMultistream.png)



> **Info**
>
> Enabling the **Use a multistream connection** replaces **Remote Video** fieldset with **Multistream Remote Videos** under the **Streams** section.
