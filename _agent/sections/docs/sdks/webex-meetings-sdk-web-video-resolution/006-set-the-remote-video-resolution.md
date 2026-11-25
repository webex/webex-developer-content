---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-video-resolution
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Set the Remote Video Resolution
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-video-resolution). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-video-resolution.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md) [System Constraints and Restrictions](005-system-constraints-and-restrictions.md)

## Article introduction

This article describes how you can set the video resolution for incoming and outgoing video streams. Resolution can be set when joining a meeting or even when a meeting is in progress.

## Selected section

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
