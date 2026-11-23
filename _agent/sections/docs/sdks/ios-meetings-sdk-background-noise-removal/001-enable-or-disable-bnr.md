---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-background-noise-removal
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Enable or Disable BNR
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-background-noise-removal). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-background-noise-removal.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use the iOS Meetings SDK background noise removal feature (BNR) to improve the quality and clarity of meeting audio.

---

You enable BNR using the `webex.phone.audioBNREnabled` property.

## Selected section

## Enable or Disable BNR

To enable or disable BNR, set `audioBNREnabled` to `true` or `false` as required:

```swift
webex.phone.audioBNREnabled = true // BNR is enabled.
```
