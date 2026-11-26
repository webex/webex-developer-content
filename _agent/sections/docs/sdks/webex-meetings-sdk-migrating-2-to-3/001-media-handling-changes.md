---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-migrating-2-to-3
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Media Handling Changes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-migrating-2-to-3). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-migrating-2-to-3.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the migration process for developers who are moving their Webex Web SDK applications from version 2 to version 3. It provides information on the most important changes to the SDK to aid our existing developers in making their applications compatible with SDK version 3.

## Selected section

## Media Handling Changes

For version 3, Tracks are migrating to Streams.

### 2.x

Media handling within the meeting object is done using the `getMediaStreams()` method. You pass audio and video device inputs along with their respective media settings, and a `Stream` object is returned:

```javascript
let currentMediaStreams = [];

const mediaSettings: {
   sendAudio: true,
   sendVideo: true,
   sendShare: false,
   receiveVideo:true,
   receiveAudio: true,
   receiveShare: true,
}

meeting.getMediaStreams(mediaSettings, audioVideoInputDevices)
  .then(([localStream, localShare]) => {

    /*
      * If you only update a particular stream, other streams return as undefined.
      * We default back to the previous stream in this case.
      */
    currentMediaStreams = [localStream, localShare];

    return currentMediaStreams;
  })
  .then(([localStream]) => {
    if (localStream && mediaSettings.sendVideo) {
      const meetingStreamsLocalVideo = new MediaStream(localStream.getVideoTracks());
      const meetingStreamsLocalAudio = new MediaStream(localStream.getAudioTracks());
    }

    return {localStream};
```

After acquiring the media streams from the respective devices, join the meeting and add the media.
```javascript
meeting.join();

meeting.addMedia({
  localShare,
  localStream,
  mediaSettings: getMediaSettings()
});
```
To stop media on a track, use the `Track` object's `stop()` method:

```javascript
audioTrack.stop();
videoTrack.stop();
```

### 3.x

In the Web SDK 3.x, we've introduced the `Stream` class. You can create a Microphone, Camera, or Display stream using the `mediaHelpers` object contained within the `meetings` object:

```javascript
// Construct the Constraints objects for audio and video...

const videoConstraints = {
    deviceId?: ConstrainDOMString;
    width?: ConstrainULong;
    height?: ConstrainULong;
    aspectRatio?: ConstrainDouble;
    frameRate?: ConstrainDouble;
    facingMode?: ConstrainDOMString;
};

const audioConstraints = {
    deviceId?: string;
    autoGainControl?: boolean;
    echoCancellation?: boolean;
    noiseSuppression?: boolean;
};

const audioStream = await webex.meetings.mediaHelpers.createMicrophoneStream(audioConstraints);
meetingStreamsLocalAudio.srcObject = audioStream;

const videoStream = await webex.meetings.mediaHelpers.createCameraStream(videoConstraints);
meetingStreamsLocalVideo.srcObject = videoStream;

// Create the display stream to share your screen, window, or tab.

const [localShareVideoStream, localShareAudioStream] = await webex.meetings.mediaHelpers.createDisplayStreamWithAudio();
```

Once you've created the above streams, you can add them to the `meeting` as shown below.



> **Info**
>
> The media settings object in version 3 varies from version 2. The example below highlights the change.



```javascript
// Join the meeting

meeting.join();

// Setup media options and add media. All the fields below are optional and boolean fields default to true unless specified otherwise
const addMediaOptions = {
  localStreams: {
    microphone: audioStream,
    camera: videoStream,
    screenShare: {
      video: localShareVideoStream,
      audio: localShareAudioStream,
    },
  },
  audioEnabled: true,
  videoEnabled: true,
  shareAudioEnabled: true,
  shareVideoEnabled: true,
  allowMediaInLobby: true,
  additionalMediaOptions: {
    sendVideo: true; // if not specified, defaults to videoEnabled value
    receiveVideo: true; // if not specified, defaults to videoEnabled value
    sendAudio: true; // if not specified, defaults to audioEnabled value
    receiveAudio: true; // if not specified, defaults to audioEnabled value
  }
};

meeting.addMedia(addMediaOptions);
```



> **Info**
>
> The additionalMediaOptions object is not applicable in multi-stream meetings.



Once media has been added to the `meeting`, in order to change the media, you must use the `unpublishStreams()` and `publishStreams()` methods in the `meeting` object.

To remove media from a `meeting` object, use the `unpublishStreams()` method:

```javascript
meeting.unpublishStreams([
  audioStream,
  videoStream
]);
```

To republish new or existing streams into the `meeting` object, use the `publishStreams()` method:

```javascript
meeting.publishStreams({microphone: audioStream, camera: videoStream}));
```
You can also use the `publishStreams()` and `unpublishStreams()` methods to start and stop sharing the screen during the meeting.

To stop the media on a stream, use the `Media` objects `stop()` method:

```javascript
audioStream.stop();

videoStream.stop();
```
