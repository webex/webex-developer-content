---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-basic-webex-calling-usage
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Place an Outgoing Call
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-basic-webex-calling-usage). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-basic-webex-calling-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the fundamental steps for integrating call functionality using the Webex iOS SDK.

## Selected section

## Place an Outgoing Call

When phone services are active, you can make outgoing calls to any Webex calling or PSTN number using `webex.phone.dialPhoneNumber()`. Note that attempting to dial non-phone numbers with `webex.phone.dialPhoneNumber()` will lead to a call failure, indicated by `INVALID_API_ERROR`:

```swift
webex.phone.dialPhoneNumber("+1800123456", option: MediaOption.audioOnly()) { result in
    switch result {
    case .success(let call):
        call.onConnected = {
            // Do something once the call is connected.
        }
        call.onDisconnected = { reason in
            // Do something on call disconnect.
        }
    case .failure(let error):
        // Call failure.
    } 
}
```



> **Info**
>
> The `dialPhoneNumber` method is available from version 3.9.2 and later.
