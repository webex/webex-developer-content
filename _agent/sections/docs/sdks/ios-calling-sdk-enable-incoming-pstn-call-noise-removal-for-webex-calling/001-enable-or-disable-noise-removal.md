---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-enable-incoming-pstn-call-noise-removal-for-webex-calling
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Enable or Disable Noise Removal
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

## Enable or Disable Noise Removal

The `call.enableReceivingNoiseRemoval()` method toggles the noise removal feature during an active call. The outcome is relayed via the `onReceivingNoiseInfoChanged` callback, confirming the action's success:

 ```swift
call.enableReceivingNoiseRemoval(shouldEnable: !receivingNoiseInfo.isNoiseRemovalEnabled) { result in
    switch result {
    case .NoError:
        print("Enable/disable ReceivingNoiseRemoval success.")
    case .NotSupported:
        print("Not supported.")
    case .InternalError:
        print("Internal error.")
    }
}
 ```
