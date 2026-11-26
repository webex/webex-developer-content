---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-video-resolution
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Set the Local Resolution Before Joining a Meeting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-video-resolution). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-video-resolution.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md) [System Constraints and Restrictions](005-system-constraints-and-restrictions.md)

## Article introduction

This article describes how you can set the video resolution for incoming and outgoing video streams. Resolution can be set when joining a meeting or even when a meeting is in progress.

## Selected section

## Set the Local Resolution Before Joining a Meeting

Before joining a meeting, the default resolution is set to **720p**. To create a camera stream with a custom resolution, use the constraints argument while creating of the `Stream` object. 

For instance, the code snippet below creates the camera stream with a resolution of **480p**.

```js
const cameraConstraints = {
  deviceId: 'deviceId',
  height: 480,
  width: 640,
};

const cameraStream = await webex.meetings.mediaHelpers.createCameraStream(cameraConstraints);
```

After joining a meeting, pass the `cameraStream` object to the `meeting` object's `addMedia()` method: 

```js
const addMediaOptions = {
  localStreams: {
    camera: cameraStream,
  },
};

await meeting.addMedia(addMediaOptions);
```



> **Info**
>
> Avoid passing anything other than the pre-defined resolutions or you'll get a `Level not supported` error. You can use custom video profiles to pass non-standard resolutions as described below.



### Create a Custom Video Profile

You can pass your own set of custom video resolution settings for different values and combinations for video to get a desired custom video resolution. For details, see [getUserMedia Parameters](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia#parameters):

```js
const constraints = {
  width: {
    max: 400,
    ideal: 400
  },
  height: {
    max: 200,
    ideal: 200
  },
  deviceId: 'e0d6eb5f9850d3f248fb717c186129fb0fd6ac35cd97feb632e0c131eb44704c',
  frameRate: {
    ideal: 10,
    max: 15
  },
  facingMode: {
    ideal: 'user' // User means the developer is asking for a video source that is facing toward the user; this includes, for example, the front-facing camera on a smartphone.
  }
};

const cameraStream = await webex.meetings.mediaHelpers.createCameraStream(constraints);
```

Available values for `facingMode` are `user`, `environment`, `left`, and `right`. For more information, see the API documentation for [facingMode](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints/facingMode).

This will create a custom camera stream, which you use to add as media after joining the meeting.

```js
const addMediaOptions = {
  localStreams: {
    camera: cameraStream,
  },
};

await meeting.addMedia(addMediaOptions);
```
