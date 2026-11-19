---
type: Guide
title: Web Meetings SDK | Video Resolution
display_title: Video Resolution
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-video-resolution
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-video-resolution)

This article describes how you can set the video resolution for incoming and outgoing video streams. Resolution can be set when joining a meeting or even when a meeting is in progress.

## Prerequisites

Keep the following prerequisites in mind:

- The device camera must support **full HD (1080p)**; if not, the feature is downgraded to the camera's maximum resolution support. To check for FHD support, see [Webcam Test Resolution](https://webcamtests.com/resolution).
- Make sure that you're using version [webex-js-sdk@2.32.0](https://github.com/webex/webex-js-sdk/compare/v2.31.4...v2.32.0) or above.



> **Info**
>
> For SDK versions 2.32.0 and above, the value mappings used for resolutions are LOW: 480p, MEDIUM: 720p, and HIGH 1080p. For earlier SDK versions: LOW: 360p, MEDIUM: 480p, and HIGH: 720p.



## Local Resolution

The sharpness, smoothness, and overall quality of the video are directly linked to the frame rate, bitrate, and other video settings. The following table specifies the different resolution settings available.

### Supported Sending Video Resolutions



| **Video Profile** | **Resolution (Width×Height)** | **Frame Rate (fps)** | **Chrome** | **Firefox** | **Safari** |
| --- | --- | --- | --- | --- | --- |
| `360p` | 640 × 360 | 30 | ✓ | ✓ | ✓ |
| `480p` | 640 × 480 | 30 | ✓ | ✓ | ✓ |
| `720p` | 1280 × 720 | 30 | ✓ | ✓ | ✓ |
| `1080p` | 1920 × 1080 | 30 | ✓ | ✓ | ✓ |

The default resolution for sending video is **720p**. You can upgrade or downgrade video resolution from the available values listed above.

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

## Set the Local Resolution During a Meeting

To change the local video resolution during a meeting, call the `applyConstraints()` method in the `Stream` object to set the new resolution.

```js
const newResolution = {
  height: 720,
  width: 1280,
}

cameraStream.applyConstraints(newResolution);
```

## System Constraints and Restrictions

Some restrictions currently affect requested video resolution while sending video:

- The camera used to capture video must be of sufficiently good quality. If a user's hardware does not capture the visual information in suitably high definition, the video quality for the remote user is similarly limited. For example, if a user sets video quality to full HD (1080p) while their device only supports 720p (HD), the SDK automatically downscales the video quality to 720p instead of the requested full HD (1080p), and the following error is logged, `Local video quality of 1080p not supported, downscaling to a highest possible resolution of 720p.`
- Check the values or range of values based upon the device or `MediaStreamTrack` using the [getCapabilities()](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack/getCapabilities) method. To retrieve the current video resolution being sent to the remote user currently, use the [getSettings](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack/getSettings)() method.
- Bandwidth and stability of the network connection limit the quality of video that is available to the remote user. In addition, there can be a slight delay between switching to a higher requested resolution from a lower resolution.
- The default setting for local video is MEDIUM (720p), and the default setting for remote video is HIGH (1080p).

## Set the Remote Video Resolution

The quality of video received by a remote user depends on video settings such as bitrate, and frame rate along with other environmental factors such as network bandwidth, device capabilities, etc.



> **Info**
>
> Due to network constraints, you may not always get the requested remote video resolution.



### Supported Remote Video Resolutions

The following remote video resolutions are supported:



| **Video Profile (Level)** | **Resolution (Width x Height)** | **Frame Rate (fps)** | **Chrome** | **Firefox** | **Safari** |
| --- | --- | --- | --- | --- | --- |
| `HIGH` | 1920 × 1080 | 30 | ✓ | ✓ | ✓ |
| `MEDIUM` | 1280 × 720 | 30 | ✓ | ✓ | ✓ |
| `LOW` | 640 × 480 | 30 | ✓ | ✓ | ✓ |

Pass one of the above-desired profile levels to the `Meeting` object's `setRemoteQualityLevel()` method to set the remote video resolution:

```js
meeting.setRemoteQualityLevel('HIGH');
```

Or

```js
meeting.setRemoteQualityLevel('LOW');
```

Keep in mind the following:

- Change to the resolution takes time to update as they upgrade or downgrade gradually depending on the quality of the network.
- If the device does not support full HD (1080p), `HIGH`, it is downscaled to the maximum supported resolution.

### Remote Video Resolution Errors

The following table lists possible errors when working with remote video resolutions:



| `Method` | `Error` | `Fix` |
| --- | --- | --- |
| `setLocalVideoTrack()` | `Meeting:index#setLocalVideoTrack --> Local video quality of "${localQualityLevel}" not supported, downscaling to the highest possible resolution of "${height}p"` | Remote resolution is set to 720p. |
| `setRemoteVideoConstraints()` | `setRemoteVideoConstraints: unable to set max framesize, value for level "${level}" is not defined` | Use the defined resolution values. |
| `getMediaStreams()` | `ParameterError: ${audioVideo} not supported. Either pass level from pre-defined resolutions or pass complete audioVideo object` | Pass a level from the pre-defined resolutions or use a complete `audioVideo` object with appropriate video properties |
| `getUserMedia()` | `Media:index#getMedia --> navigator.mediaDevices.getUserMedia failed - [object OverconstrainedError] (facingMode)` | If you request the rear camera on a laptop device, you'll get this error. Use either `ideal` instead of `exact` or request only cameras appropriate to the device. |
