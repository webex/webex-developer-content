---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-background-noise-removal
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
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
