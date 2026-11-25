---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-additional-methods
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Bandwidth Extension / Speech Enhancement
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-additional-methods). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-additional-methods.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article describes additional methods available in the Webex Calling Android SDK.

---



> **Info**
>
> The Mobile SDK supports a maximum of two concurrent incoming calls. A third incoming call is automatically ignored or silently dismissed. Only one call can be in a resumed state at any time.

## Selected section

## Bandwidth Extension / Speech Enhancement

The Bandwidth Extension Support feature allows developers to enhance receiver-side audio quality during WebexCalling and CUCM calls. These APIs are available from SDK v3.14 onwards.

### Phone-Level APIs (Before a Call)

Use these APIs before making a call.

#### Enable Legacy Receiver Noise Removal

```kotlin
// Enable legacy receiver noise removal
webex.phone.useLegacyReceiverNoiseRemoval(true)

// Disable legacy receiver noise removal to use new speech enhancement
webex.phone.useLegacyReceiverNoiseRemoval(false)
```

#### Check if Speech Enhancement Is Enabled by Default

```kotlin
// Check if speech enhancement is enabled by default
var isEnabled = webex.phone.isReceiverSpeechEnhancementEnabled()
```

#### Enable/Disable Speech Enhancement by Default

```kotlin
// Enable speech enhancement by default for all calls
webex.phone.enableReceiverSpeechEnhancement(true) {
    if (it.isSuccessful) {
        // Speech Enhancement was successfully set
    } else {
        // Handle error
    }
}

// Disable speech enhancement by default for all calls
webex.phone.enableReceiverSpeechEnhancement(false) {
    if (it.isSuccessful) {
        // Speech Enhancement was successfully set
    } else {
        // Handle error
    }
}
```

### Call-Level APIs (During a Call)

Use these APIs while in an active call.

#### Check if Speech Enhancement Is Enabled for the Current Call

```kotlin
// Check if speech enhancement is enabled for the current call
var isEnabled = call.isReceiverSpeechEnhancementEnabled
```

#### Enable/Disable Speech Enhancement for the Current Call

```kotlin
// Enable speech enhancement for the current call
call.enableReceiverSpeechEnhancement(true) {
    if (it.isSuccessful) {
        // Speech Enhancement was successfully set
    } else {
        // Handle error
    }
}

// Disable speech enhancement for the current call
call.enableReceiverSpeechEnhancement(false) {
    if (it.isSuccessful) {
        // Speech Enhancement was successfully set
    } else {
        // Handle error
    }
}
```
