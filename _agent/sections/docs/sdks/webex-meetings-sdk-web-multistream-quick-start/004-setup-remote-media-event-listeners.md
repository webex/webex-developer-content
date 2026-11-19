---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-multistream-quick-start
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Setup Remote Media Event Listeners
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-multistream-quick-start). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-multistream-quick-start.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

With multistream, developers gain greater flexibility when displaying remote media streams. Instead of receiving a single stream featuring all participants, multistream enables the showcasing of multiple streams simultaneously. This means you can easily view each remote participant's stream individually, enhancing clarity and engagement during collaborative sessions.

---

This guide provides a quick glimpse into consuming multistream in Webex Meetings using the Webex JavaScript SDK. You'll find code snippets below that can quickly get you up and running.

## Selected section

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
