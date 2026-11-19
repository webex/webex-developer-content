---
type: Guide
title: Android Calling SDK | Enable Incoming PSTN Call Noise Removal for Webex Calling
display_title: PSTN Noise Removal
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-enable-incoming-pstn-call-noise-removal-for-webex-calling
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-calling-sdk-enable-incoming-pstn-call-noise-removal-for-webex-calling)

Developers can improve the audio quality of incoming PSTN (Public Switched Telephone Network) or phone calls by enabling the far-end noise removal feature.

---

Noise removal is beneficial when the PSTN caller lacks access to noise removal technology. Once enabled, SDK users will experience clearer incoming audio without background noise.



> **Info**
>
> This feature is available for both WebexCalling (WxC) and CUCM (Cisco Unified Communications Manager) calls in Android SDK versions 3.9.0 and later.



## Enable or Disable Noise Removal

The `call.enableReceivingNoiseRemoval()` method toggles the noise removal feature during an active call. The outcome is relayed via the `onReceivingNoiseInfoChanged` callback, confirming the action's success:

```kotlin
call.enableReceivingNoiseRemoval(enable, callback)
```

## Handle the Noise Information Callback

The `CallObserver.onReceivingNoiseInfoChanged()` callback provides updates regarding noise detection and the status of the noise removal feature. This callback is part of the `CallObserver` interface, which is set up using the `Call.setObserver()` method.

The `ReceivingNoiseInfo` object contains two important properties:

* `isNoiseDetected`: This boolean indicates if any background noise is detected in the incoming call. When noise is detected, the `enableReceivingNoiseRemoval` method should be invoked to activate noise removal.
* `isNoiseRemovalEnabled`: This boolean signifies whether the noise removal feature is currently active. If true, any noise detected in the incoming call will be filtered out.

The `onReceivingNoiseInfoChanged` callback is triggered under two circumstances:

1. When the call is initially connected, signaling the availability of the noise removal feature for the call with both `isNoiseDetected` and `isNoiseRemovalEnabled` set to `false`.
1. Whenever there is a change in the `isNoiseDetected` or `isNoiseRemovalEnabled` values. For example, the callback fires when noise removal is activated or deactivated, or when new background noise is detected.

Here is an example of setting the call observer:

```kotlin
val mediaOption = MediaOption.audioOnly()
webex.phone.dial("+1800123456", mediaOption, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Dial method successful.
        val call = result.data
        call?.setObserver(object : CallObserver {
            override fun onReceivingNoiseInfoChanged(info: ReceivingNoiseInfo) {
                // Use the info object to take further action.
            }
        })
    } else {
        // Dial failed
    }
})
```

To obtain the current `ReceivingNoiseInfo` object, use the `getReceivingNoiseInfo()` method:

 ```kotlin
 val infoObject = call.getReceivingNoiseInfo()
 logDebug("$tag ReceivingNoiseRemoval : ", infoObject.toString())
 ```
