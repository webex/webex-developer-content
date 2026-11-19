---
type: Guide
title: Web Meetings SDK | Migrating SDK Version 2 to Version 3
display_title: Migrating SDK V2 to V3
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-migrating-2-to-3
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-meetings-sdk-migrating-2-to-3)

This article outlines the migration process for developers who are moving their Webex Web SDK applications from version 2 to version 3. It provides information on the most important changes to the SDK to aid our existing developers in making their applications compatible with SDK version 3.

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

## Media Event Payload Changes

### 2.x

In the version 2 SDK, the `media:ready` and `media:stop` events on the meeting object return a payload containing the following media types:

- `remoteVideo`
- `remoteAudio`
- `remoteShare`
- `localShare`

The second part of the payload includes `MediaStream` object.

### 3.x

In version 3 SDK, the `localShare` media type is no longer passed as a type in the media event payload.

## Media Effect Upgrades and Changes

### 2.x

In version 2 of the SDK, the `meeting` object exposes the Background Noise Removal (BNR) functionality to developers. To enable or disable this functionality, after adding audio tracks to the meeting:

```javascript
meeting.enableBNR();
meeting.disableBNR();
```

### 3.x

In version 3 of the SDK, developers have access to additional media effects features:

- Background Noise Removal
- Custom Virtual Background
- Blur

All the above effects are now exposed as their own classes via the SDK. These effects are applied to the `Stream` objects created at the start of the meeting flow.

## Stream Mute Options

To accommodate the distinction between muting devices programmatically and muting them via a physical button, modifications have been made to the APIs associated with LocalStream and RemoteStream. Some devices, such as Chromebooks, have a physical button that allows users to mute and unmute their microphone or camera. When a device is muted using this physical button, it cannot be unmuted programmatically; the user must manually press the button again to unmute it.

The API changes ensure that developers can identify the mute state accurately and respond appropriately within their applications, regardless of whether the mute action was initiated by software or hardware.



> **Info**
>
> This breaking change is part of version `webex@3.0.0-next.10` and later.



### LocalTrack's `setMuted` method
#### 2.x

This is the method that is to be used to programmatically mute a `LocalTrack` in the V2 SDK.

```javascript
localTrack.setMuted(true); // Set to false in order to unmute.
```

#### 3.x

In the V3 SDK, this method is renamed as follows:

```javascript
localStream.setUserMuted(true); // Set to false in order to unmute.
```

### LocalTrack's `mute-state-change` event
#### 2.x

This event is triggered when the mute state of a local track changes programmatically.

```javascript
localTrack.on('mute-state-change', (isMuted) => {
  // Update the UI to reflect the mute state change.
});
```

#### 3.x
The `mute-state-change` event is replaced and split into two:

**`user-mute-state-change`**
This is the event that's fired when the mute state changes programmatically.

```javascript
localStream.on('user-mute-state-change', (isUserMuted) => {
  // This handler is triggered when the user toggles the mute programmatically.
  // 'isUserMuted' indicates the new mute state: true for muted, false for unmuted.
});
```

**`system-mute-state-change`**
This is the event that's fired when the mute state changes through a physical button.

```javascript
localStream.on('system-mute-state-change', (isSystemMuted) => {
  // Triggered when the user mutes through a physical button.
  // At this point, it is important to note that the unmute button won't work if 'isSystemMuted' is true.
  // You can use this to disable the unmute button and add a UI note stating that the user has to unmute their hardware.
});
```

### LocalTrack's `muted` getter
This remains unchanged. It will return true in either case (programmatically muted or hardware muted).

#### 3.x

However, in 3.x, two new getters are introduced:
- `LocalStream.userMuted` - true when programmatically muted
- `LocalStream.systemMuted` - true when muted via hardware

### RemoteTrack's `muted` getter

#### 2.x
This getter is used to identify if a remote track is muted or not.

```javascript
const isRemoteMuted = remoteTrack.muted;
```

#### 3.x
The `muted` is replaced by the `mediaState` getter which can be used as follows,

```javascript
const isRemoteMuted = remoteStream.mediaState !== 'started';
```

Basically, the getter `remoteStream.mediaState` will return either `started` or `stopped`, meaning the stream is not muted or muted, respectively.

### RemoteTrack's `mute-state-change` event

#### 2.x

This event is subscribed to in order to know if the remote track's mute state changes.

```javascript
remoteTrack.on('mute-state-change', (isMuted) => {
  // Implement functionality to handle mute state change.
  // 'isMuted' indicates whether the remote track is muted or not.
});
```

#### 3.x

The existing `mute-state-change` event is replaced with the `media-state-change` event, and it can be used as follows:

```javascript
remoteStream.on('media-state-change', (mediaState) => {
  // 'mediaState' can be either 'started' or 'stopped'.
  // 'started' indicates the media is unmuted.
  // 'stopped' indicates the media is muted.
  
  // Implement the logic based on the media state.
  if (mediaState === 'started') {
    // Handle the unmuted state.
  } else if (mediaState === 'stopped') {
    // Handle the muted state.
  }
});
```

## Frequently Asked Questions

As you prepare to upgrade, we've compiled some key questions and answers to streamline your transition. This guide will help you navigate the new features, address the breaking changes, and ensure a smooth update process. If further assistance is needed, our support team is ready to assist you.

**1. What is the Webex Web SDK V3?**

The Webex Web SDK V3 is the newest Meetings SDK launched as part of the Webex Developer Platform. It introduces various new capabilities and features.

**2. What's new in V3?**

V3 SDK introduces:

- Closed captions for live transcriptions.
- Improved background noise reduction.
- Virtual background effect supporting background blur, virtual image, and virtual video.

**3. What are the differences between V1/V2 and V3?**

Key differences include:

- Handling of local media.
- The payload for the `media:ready` event.
- Audio and video effects.
- Stream mute events and methods.
- Migration to improved meetings experience (available since V2.60.0).
- Multistream support.

**4. Will V1/V2 of the Webex Web SDK still be supported, and for how long?**

Support for the V1 SDK has ended. The V2 SDK will reach End of Life (EoL) by November 1, 2024, and will be supported until that date.

**5. Are there any tools or scripts provided to facilitate the migration process?**

Currently, no tool or script is available to assist with this migration due to the unique ways applications use the SDK.

**6. Can I run V1/V2 and V3 SDKs in parallel during the transition?**

Running V1/V2 and V3 SDKs in parallel is not advised and not supported, as this setup has not been tested.

**7. Are there any known issues or limitations in V3 that I should be aware of before migrating?**

Known limitations include:

- Screen sharing with tab audio is not supported during Transcoded meetings, but it is supported in Multistream settings.
- Screen sharing using Firefox may freeze when sharing the entire screen.

**8. What are the system and browser requirements for V3?**

- **Browser:** Compatible with all Chromium and Webkit-based browsers, including Google Chrome, Microsoft Edge, and Apple Safari.
- **NodeJS:** For the Node version of the Webex SDK, ensure your app's node versions are:
  - Node - 16.x
  - NPM - 6.x or later

**9. Are there any changes in the method signature or event payloads in V3?**

Response formats remain unchanged. However, there are request changes for:

- Method: Input changes for the `meeting.addMedia` method.
- Event: Changed payload for the `media:ready` event on the meeting object.

For more details, read the [here](#media-event-payload-changes).

**10. What is a Transcoded meeting?**

A transcoded meeting involves the Webex cloud combining video streams from all participants into a single stream transmitted to clients.

**11. What is a Multistream meeting?**

A multistream meeting allows the Webex cloud to send individual video streams from all participants to clients, enabling customized stream layouts.

Here's the [Quick Start guide to Multistream meetings](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-multistream-quick-start).

**12. Is there any change in the licensing or pricing for the use of V3?**

Refer to the [SDK LICENSE](https://github.com/webex/webex-js-sdk/blob/next/LICENSE.md).

**13. How to avail support during and after migrating to V3?**

Reach out to the SDK team through:

- [Developer Support](https://developer.webex.com/support)
- [Developer Community](https://community.cisco.com/t5/webex-for-developers/bd-p/disc-webex-developers)
- [GitHub Repository Issues](https://github.com/webex/webex-js-sdk/issues) - (Issues, Q&A, Features)
- Email - [devsupport@webex.com](mailto:devsupport@webex.com)

These channels can also be used to report bugs in the V3 SDK.

**14. Where can I find documentation for the new V3 features?**

The Webex Meetings SDK documentation is available here: [Webex Web Meetings SDK](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction).

**15. Are there any other resources?**

Additional resources include:

- **Webinar:** [Upgrade Your App with Webex Meetings SDK V3 Simplified Integration and Enhanced Features](https://app.vidcast.io/share/bcd28aa8-ab52-46bc-8ca8-3c2aa41f8f83)
- **Meetings Demo app:** Access the [source code to the demo application](https://github.com/WebexSamples/webex-js-sdk-meeting-demo/) from the webinar.
- **Vidcast:** [Kitchen Sink App Walkthrough](https://app.vidcast.io/share/e88ad798-d911-4e25-a5ba-c4f75740d2c3)
- **Kitchen Sink App:** Test various features using our [Kitchen Sink app](https://webex.github.io/webex-js-sdk/). The source code is available [here](https://github.com/webex/webex-js-sdk/tree/next/docs/samples).

**16. What is Improved Meetings Experience?**

The improved meetings experience combines **Webex Meetings** (Scheduled Webex Meetings, PMR) and **Space Meetings** (Scheduled Space Meetings, Instant Space Meetings).

Discover more about it here: [Webex App | Improved meetings associated with a space](https://help.webex.com/en-us/article/gxw5jz/Webex-App-%7C-Improved-meetings-associated-with-a-space)

**17. Does Migration to Improved Meetings Experience require only SDK upgrade?**

No, organization-level changes are also necessary for the new, improved meetings experience. Learn more about it:

- [Migrating to Improved Meetings Experience](https://developer.webex.com/docs/space-meetings-migration)
- [Web SDK: Migration to Improved Meetings Associated with a Space](https://github.com/webex/webex-js-sdk/wiki/Migration-to-improved-meetings-associated-with-a-space)

**18. When is EoL for the Old Meetings Experience?**

The EoL for the Old Meetings Experience is set for July 1, 2024. Organizations should complete their migration before this date.

**19. The EoL for Old Meetings Experience is conflicting with EoL of V2 SDK. I'm confused**

Here's a clearer timeline:

- Old Meetings Experience
  - Supported by Web SDK until **V2.60.0**
  - End of Life - July 1, 2024
- Web SDK V2
  - Supports Improved Meetings Experience from **V2.60.0**
  - End of Life - November 1, 2024

If you're planning to migrate from the Old Meetings Experience and can transition to Web SDK V3, it's recommended to migrate to V3 and the Improved Meetings Experience at the same time. If you need more time for V3, upgrade to Web SDK V2.60.0 or a later V2 version before July 1, 2024, and plan a separate migration to V3 SDK.
