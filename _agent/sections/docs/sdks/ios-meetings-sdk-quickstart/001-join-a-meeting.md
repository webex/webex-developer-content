---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-quickstart
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Join a Meeting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide provides examples of common methods used in the meetings flow for the iOS Meetings SDK. For detailed method parameters, refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/ios-sdk-overview#sdk-api-reference).

---

The `Webex` instance is the core access point for the SDK, providing access to all Webex SDK methods. A `Call` object represents a meeting and includes methods for joining, leaving, muting, unmuting, and other actions. This object is returned as a result of a successful `dial` method invocation.

## Selected section

## Join a Meeting

Use the `dial` method to join a meeting by passing a meeting ID, SIP address, or meeting link:

```swift
webex.phone.dial("meetingId", option: MediaOption.audioVideo(local: ..., remote: ...)) { result in
    switch result {
    case .success(let call):
        call.onConnected = {
            // ...
        }
        call.onDisconnected = { reason in
            // ...
        }
    case .failure(let error):
        // failure
    }
}
```
