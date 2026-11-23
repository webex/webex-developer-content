---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-background-noise-removal
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Configure the BNR Mode
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-background-noise-removal). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-background-noise-removal.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use the iOS Meetings SDK background noise removal feature (BNR) to improve the quality and clarity of meeting audio.

---

You enable BNR using the `webex.phone.audioBNREnabled` property.

## Selected section

## Configure the BNR Mode

The BNR feature supports two modes: Low Power (LP) and High Performance (HP).

```swift
enum AudioBNRMode {
    case LP // Low Power
    case HP // High Performance
}
```

Set the BNR mode to `.HP` by default.



> **Info**
>
> The BNR mode is only effective if `webex.phone.audioBNREnabled` is set to `true`.



```swift
webex.phone.audioBNRMode = .HP
```
