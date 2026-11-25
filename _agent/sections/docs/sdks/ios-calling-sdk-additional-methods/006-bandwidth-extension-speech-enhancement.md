---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-additional-methods
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Bandwidth Extension / Speech Enhancement
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

## Bandwidth Extension / Speech Enhancement

The Bandwidth Extension Support feature allows developers to enhance receiver-side audio quality during WebexCalling and CUCM calls. These APIs are available from SDK v3.14 onwards.

### Phone Class APIs (Before a Call)

#### Enable Legacy Receiver Noise Removal

```swift
// Enable legacy receiver noise removal
Webex.phone.useLegacyReceiverNoiseRemoval(useLegacy: true)

// Disable legacy receiver noise removal to use new speech enhancement
Webex.phone.useLegacyReceiverNoiseRemoval(useLegacy: false)
```

#### Check if Speech Enhancement Is Enabled by Default

```swift
// Check if speech enhancement is enabled by default
let isEnabled = Webex.phone.isReceiverSpeechEnhancementEnabled
```

#### Enable/Disable Speech Enhancement by Default

```swift
// Enable speech enhancement by default for all calls
Webex.phone.enableReceiverSpeechEnhancement(shouldEnable: true) { result in
    switch result {
    case .success:
        print("Speech enhancement enabled by default")
    case .failure(let error):
        print("Failed to enable speech enhancement: \(error)")
    }
}

// Disable speech enhancement by default for all calls
Webex.phone.enableReceiverSpeechEnhancement(shouldEnable: false) { result in
    switch result {
    case .success:
        print("Speech enhancement disabled by default")
    case .failure(let error):
        print("Failed to disable speech enhancement: \(error)")
    }
}
```

### Call Class APIs (During a Call)

#### Check if Speech Enhancement Is Enabled for the Current Call

```swift
// Check if speech enhancement is enabled for the current call
let isEnabled = Webex.call.isReceiverSpeechEnhancementEnabled
```

#### Enable/Disable Speech Enhancement for the Current Call

```swift
// Enable speech enhancement for the current call
Webex.call.enableReceiverSpeechEnhancement(shouldEnable: true) { result in
    switch result {
    case .success:
        print("Speech enhancement enabled for the call")
    case .failure(let error):
        print("Failed to enable speech enhancement: \(error)")
    }
}

// Disable speech enhancement for the current call
Webex.call.enableReceiverSpeechEnhancement(shouldEnable: false) { result in
    switch result {
    case .success:
        print("Speech enhancement disabled for the call")
    case .failure(let error):
        print("Failed to disable speech enhancement: \(error)")
    }
}
```
