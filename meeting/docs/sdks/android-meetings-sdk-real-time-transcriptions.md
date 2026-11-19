---
type: Guide
title: Android Meetings SDK | Real-Time Transcriptions
display_title: Real-Time Transcriptions
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-real-time-transcriptions
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-meetings-sdk-real-time-transcriptions)

Enable Real-Time Transcription (RTT) during Webex meetings using the Webex Assistant (WXA).

---

Hosts can activate or deactivate WXA before or during a meeting. With RTT SDK methods, users can control WXA to view live transcriptions.



> **Info**
>
> RTT is available starting from SDK version 3.3.0.



## Enable Real-Time Transcriptions

To enabled real-time transcriptions:

1. Check to see if the Webex Assistant is enabled:

    ```kotlin
    val isEnabled: Boolean = call.getWXA().isEnabled()
    ```

1. Verify that the user can control the Webex Assistant:

    ```kotlin
    val canControl = call.getWXA().canControlWXA()
    ```

    ![WXA Control](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt25084d348535731b/can-control-wxa.gif)

1. If the Webex Assistant is disabled, enable it:

    ```kotlin
    call.getWXA().enableWXA(true /*true to enable otherwise false*/, CompletionHandler { result ->
        Log.d(TAG, "enableWXA callback: result ${result.isSuccessful} isEnabled ${result.data}")
    })
    ```

    ![Enable WXA](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt252937aa5fafcafb/enable-wxa.gif)

1. Register for transcription updates:

    ```kotlin
    call.getWXA()?.setOnTranscriptionArrivedListener( object :
        WXA.OnTranscriptionArrivedListener {
            override fun onTranscriptionArrived(transcription: Transcription) {
                Log.d(TAG, 
                "transcription: ${transcription.content} by ${transcription.personName}")
            }
    })
    ```

    ![RTT transcription updates](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte67771647dd822c8/transcriptions-list.gif)
