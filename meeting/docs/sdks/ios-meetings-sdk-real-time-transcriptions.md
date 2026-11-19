---
type: Guide
title: iOS Meetings SDK | Real-Time Transcriptions
display_title: Real-Time Transcriptions
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-real-time-transcriptions
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-meetings-sdk-real-time-transcriptions)

Enable Real-Time Transcription (RTT) during Webex meetings using the Webex Assistant (WXA).

---

Hosts can activate or deactivate WXA before or during a meeting. With RTT SDK methods, users can control WXA to view live transcriptions.



> **Info**
>
> RTT is available starting from SDK version 3.3.0.





> **Info**
>
> From SDK version 3.17.0, the Webex Assistant methods no longer require a feature toggle to be enabled for the user. On earlier versions, `isEnabled` and `canControlWXA` returned `false` when that toggle was off.



To enable RTT:

1. Check to see if the Webex Assistant is enabled:

    ```swift
    var isEnabled = call.wxa.isEnabled
    ```

1. Verify that the user can control the Webex Assistant:

    ```swift
    var canControl = call.wxa.canControlWXA 
    ```

    ![WXA Control](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt16c28f9e76f61390/wxa-can-control.gif)

1. If the Webex Assistant is disabled, enable it:

    ```swift
    call.wxa.enableWXA(isEnabled: isWXAEnabled, callback: { success in
        print("setting WXA to: \(isWXAEnabled) operation returned: \(success)")
    })
    ```

    ![Enable WXA](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt07c7f85168f8dfea/wxa-enable.gif)

1. Register for transcription updates:

    ```swift
    call.wxa.onTranscriptionArrived = { transcription in
        // ....
    }
    ```

    ![RTT transcription updates](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt89d5c3178e791dc5/wxa-rtt-reception.gif)
