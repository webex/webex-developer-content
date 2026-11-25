---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-additional-methods
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Sign In to Phone Services
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

## Sign In to Phone Services

To connect to Webex calling phone services:

```swift
webex.phone.connectPhoneServices(completionHandler: { result in
    switch result {
    case .success:
        // PhoneServices connected successfully.
    case .failure:
        // PhoneServices connection failed.
    }
})
```

The phone service status updates are provided via the `onUCServerConnectionStateChanged` callback.
