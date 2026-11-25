---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-video-resolution
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Local Resolution
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-video-resolution). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-video-resolution.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md) [System Constraints and Restrictions](005-system-constraints-and-restrictions.md)

## Article introduction

This article describes how you can set the video resolution for incoming and outgoing video streams. Resolution can be set when joining a meeting or even when a meeting is in progress.

## Selected section

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
