---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-enable-incoming-pstn-call-noise-removal-for-webex-calling
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Handle the Noise Information Callback
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-enable-incoming-pstn-call-noise-removal-for-webex-calling). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-enable-incoming-pstn-call-noise-removal-for-webex-calling.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Developers can improve the audio quality of incoming PSTN (Public Switched Telephone Network) or phone calls by enabling the far-end noise removal feature.

---

Noise removal is beneficial when the PSTN caller lacks access to noise removal technology. Once enabled, SDK users will experience clearer incoming audio without background noise.



> **Info**
>
> This feature is available for both WebexCalling (WxC) and CUCM (Cisco Unified Communications Manager) calls in iOS SDK versions 3.9.0 and later.

## Selected section

## Handle the Noise Information Callback

The `Call.onReceivingNoiseInfoChanged` callback provides updates regarding noise detection and the status of the noise removal feature.

The `ReceivingNoiseInfo` object contains two important properties:

* `isNoiseDetected`: This boolean indicates if any background noise is detected in the incoming call. When noise is detected, the `enableReceivingNoiseRemoval` method should be invoked to activate noise removal.
* `isNoiseRemovalEnabled`: This boolean signifies whether the noise removal feature is currently active. If true, any noise detected in the incoming call will be filtered out.

The `onReceivingNoiseInfoChanged` callback is triggered under two circumstances:

1. When the call is initially connected, signaling the availability of the noise removal feature for the call with both `isNoiseDetected` and `isNoiseRemovalEnabled` set to `false`.
1. Whenever there is a change in the `isNoiseDetected` or `isNoiseRemovalEnabled` values. For example, the callback fires when noise removal is activated or deactivated, or when new background noise is detected.

Here is an example of setting the call observer and handling the noise information:

Set the `onReceivingNoiseInfoChanged` observer:

```swift
call.onReceivingNoiseInfoChanged = { info in
    print("Noise information callback triggered.")
}
```  

Access `ReceivingNoiseInfo`:

```swift
val infoObject = call.receivingNoiseInfo
```
