---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-1080p-resolution-support
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Capture Full HD Video
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-1080p-resolution-support). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-1080p-resolution-support.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Enabling 1080p video resolution (Full HD) is possible for 1-1 calls, space meetings, and Webex meetings by setting the preferred maximum video bandwidth to 1080p.

---



> **Info**
>
> Supported by version 3.5.0 and later of the Android SDK.

## Selected section

## Capture Full HD Video

To enable full HD video capture:

```kotlin
webex.phone.setVideoMaxTxBandwidth(Phone.DefaultBandwidth.MAX_BANDWIDTH_1080P.getValue())
```
