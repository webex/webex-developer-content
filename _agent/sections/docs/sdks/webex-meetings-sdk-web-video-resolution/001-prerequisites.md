---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-video-resolution
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Prerequisites
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-video-resolution). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-video-resolution.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [System Constraints and Restrictions](005-system-constraints-and-restrictions.md)

## Article introduction

This article describes how you can set the video resolution for incoming and outgoing video streams. Resolution can be set when joining a meeting or even when a meeting is in progress.

## Selected section

## Prerequisites

Keep the following prerequisites in mind:

- The device camera must support **full HD (1080p)**; if not, the feature is downgraded to the camera's maximum resolution support. To check for FHD support, see [Webcam Test Resolution](https://webcamtests.com/resolution).
- Make sure that you're using version [webex-js-sdk@2.32.0](https://github.com/webex/webex-js-sdk/compare/v2.31.4...v2.32.0) or above.



> **Info**
>
> For SDK versions 2.32.0 and above, the value mappings used for resolutions are LOW: 480p, MEDIUM: 720p, and HIGH 1080p. For earlier SDK versions: LOW: 360p, MEDIUM: 480p, and HIGH: 720p.
