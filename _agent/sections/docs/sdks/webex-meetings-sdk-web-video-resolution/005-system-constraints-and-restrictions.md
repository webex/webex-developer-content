---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-video-resolution
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- System Constraints and Restrictions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-video-resolution). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-video-resolution.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article describes how you can set the video resolution for incoming and outgoing video streams. Resolution can be set when joining a meeting or even when a meeting is in progress.

## Selected section

## System Constraints and Restrictions

Some restrictions currently affect requested video resolution while sending video:

- The camera used to capture video must be of sufficiently good quality. If a user's hardware does not capture the visual information in suitably high definition, the video quality for the remote user is similarly limited. For example, if a user sets video quality to full HD (1080p) while their device only supports 720p (HD), the SDK automatically downscales the video quality to 720p instead of the requested full HD (1080p), and the following error is logged, `Local video quality of 1080p not supported, downscaling to a highest possible resolution of 720p.`
- Check the values or range of values based upon the device or `MediaStreamTrack` using the [getCapabilities()](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack/getCapabilities) method. To retrieve the current video resolution being sent to the remote user currently, use the [getSettings](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack/getSettings)() method.
- Bandwidth and stability of the network connection limit the quality of video that is available to the remote user. In addition, there can be a slight delay between switching to a higher requested resolution from a lower resolution.
- The default setting for local video is MEDIUM (720p), and the default setting for remote video is HIGH (1080p).
