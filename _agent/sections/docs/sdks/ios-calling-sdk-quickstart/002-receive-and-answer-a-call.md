---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-quickstart
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Receive and Answer a Call
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide provides the fundamental steps for integrating calling features into your iOS application using the Webex iOS Mobile SDK. For comprehensive parameters and methods, please refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/ios-sdk-overview#sdk-api-reference).

---

At the core of the SDK is the `Webex` object, serving as the gateway to all SDK functionalities. The `Call` object represents an active call and provides methods to manage various aspects of the call lifecycle, such as answering, hanging up, muting, and unmuting. You obtain a `Call` object either as a result of a successful outgoing call through the `dial` method or as an incoming call event.

## Selected section

## Receive and Answer a Call

Incoming calls are handled by setting a listener on the `onIncoming` event of the `phone` object:

```swift
webex.phone.onIncoming = { call in
    call.answer(option: MediaOption.audioVideo(local: ..., remote: ...)) { error in
    if let error = error {
        // failure
    }
    else {
        // success
    }
}
```
