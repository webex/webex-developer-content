---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-additional-methods
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- External Tracking ID Retrieval
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-additional-methods). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-additional-methods.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article describes additional methods available in the Webex Calling iOS SDK.

---



> **Info**
>
> The Mobile SDK supports a maximum of two concurrent incoming calls. A third incoming call is automatically ignored or silently dismissed. Only one call can be in a resumed state at any time.

## Selected section

## External Tracking ID Retrieval

To obtain an `externalTrackingId` for call logging and metrics:

```swift
call.externalTrackingId
// Use the trackingId after the onInfoChanged callback has fired.
```
