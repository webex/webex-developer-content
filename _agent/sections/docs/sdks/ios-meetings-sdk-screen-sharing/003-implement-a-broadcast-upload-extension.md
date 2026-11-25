---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-screen-sharing
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Implement a Broadcast Upload Extension
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-screen-sharing). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-screen-sharing.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex iOS Meetings SDK allows you to share the entire screen of your iOS mobile device during a call or meeting.

---

This article guides your through implementing screen sharing in your own iOS application.

## Selected section

## Implement a Broadcast Upload Extension



> **Info**
>
> This procedure was developed using Xcode 8 and iOS 11.2.



To implement a broadcast upload extension:

1. Set up your own App Group by following this [guide](https://github.com/webex/webex-ios-sdk/wiki/Setting-App-Group) to enable the App Group capability and name it. This will be used in steps 4 and 5.

2. In Xcode, go to **File -> New -> Target -> iOS Application Extension** and select **Broadcast Upload Extension** to create a new extension target. The Broadcast Setup UI Extension is optional.

3. Modify your project's `Podfile` to add `WebexBroadcastExtensionKit` for your broadcast extension target. Run `pod install` or `pod update` from your project directory:

    

> **Warning**
>
> On December 2, 2026, CocoaPods trunk will stop accepting new pod versions. Existing CocoaPods integrations will keep working, but you must use Swift Package Manager to get later Webex iOS SDK releases. See the [CocoaPods trunk read-only plan](https://blog.cocoapods.org/CocoaPods-Specs-Repo/).



    ```swift
    target 'SDKExampleBroadcastExtension' do
        platform :ios, '15.0'
        pod 'WebexBroadcastExtensionKit'
    end
    ```

If you use Swift Package Manager with WebexSDK 3.17.0 or later, which requires an iOS 15 or later deployment target, add the `WebexBroadcastExtensionKit` product to the broadcast extension target instead of editing a `Podfile`, and add `import WebexBroadcastExtensionKit` to `SampleHandler.swift`. Attach it to the extension target only, never to the app target.

4. In Xcode, locate `SampleHandler.swift` in your broadcast extension folder. Use the SDK broadcast extension method to enable screen sharing. Add your app and extension to the same App Group and pass the App Group Identifier to the SDK:

    ```swift
    WebexBroadcastExtension.sharedInstance.start(applicationGroupIdentifier: "group.your.application.group.identifier") { error in
        // Handle any errors here
    }
    ```

5. End the broadcast when the extension ends or at any desired point:

    ```swift
    override func broadcastFinished() {
        // User has requested to finish the broadcast.
        WebexBroadcastExtension.sharedInstance.finish()
    }
    ```

6. When the system delivers the video sample buffer to your extension, call the SDK's `handleVideoSampleBuffer` method:

    ```swift
    override func processSampleBuffer(_ sampleBuffer: CMSampleBuffer, with sampleBufferType: RPSampleBufferType) {
        switch sampleBufferType {
            case RPSampleBufferType.video:
                // Handle video sample buffer
                WebexBroadcastExtension.sharedInstance.handleVideoSampleBuffer(sampleBuffer: sampleBuffer)
            case RPSampleBufferType.audioApp:
                // Handle audio sample buffer for app audio
                break
            case RPSampleBufferType.audioMic:
                // Handle audio sample buffer for mic audio
                break
        }
    }
    ```

7. Observe the broadcast server state changes and handle errors from the containing app:

    ```swift
    WebexBroadcastExtension.sharedInstance.onError = { error in
        switch error {
        case .illegalOperation(let reason):
            // The request is illegal.
            break
        case .illegalStatus(let reason):
            // The request is in an illegal status.
            break
        case .serviceFailed(let code, let reason):
            // A request to the Webex SDK containing app failed.
            break
        }
    }

    WebexBroadcastExtension.sharedInstance.onStateChange = { state in
        switch state {
        case .Initiated:
            break
        case .Broadcasting:
            // Connected with the containing app broadcast server.
            break
        case .Suspended:
            // The containing app broadcast server connection is suspended.
            break
        case .Stopped:
            break
        }
    }
    ```

    Refer to this sample for WebexBroadcastExtension usage: [WebexBroadcastExtension Demo](https://github.com/webex/webex-ios-sdk-example/blob/master/KitchenSinkBroadcastExtension/SampleHandler.swift).

8. Use `call.oniOSBroadcastingChanged` to monitor the connection status of the user's broadcast extension:

    ```swift
    call.oniOSBroadcastingChanged = { event in
        switch event {
        case .extensionConnected:
            // Handle extension connected
            break
        case .extensionDisconnected:
            // Handle extension disconnected
            break
        }
    }
    ```

9. Once the broadcast extension is connected, start and stop screen sharing with:

    ```swift
    call.startSharing { error in
        // Handle any errors
    }
    ```

    ```swift
    call.stopSharing { error in
        // Handle any errors
    }
    ```

    

> **Info**
>
> The complete demo app is available on this GitHub [repo](https://github.com/webex/webex-ios-sdk-example/).



10. To run your Broadcast extension:
    - Add screen recording to Control Center: Open **Settings -> Control Center -> Customize Controls**. Tap the '+' next to **Screen Recording**.
    - Start your broadcast extension: Swipe up to open Control Center. Long press the recording button. Select your extension, then tap **Start Broadcast**.

11. To debug your app extension:
    - If debugging your app with Xcode, attach to the app extension process when it starts. Go to **Xcode -> Debug -> Attach to Process -> [Your Broadcast Extension]**.
    - Alternatively, use **Debug -> Attach to Process -> By Process Identifier (PID) or Name...**, enter your app extension's name, and Xcode will attach to it automatically when started.

### Development Tips for App Extensions

1. App extensions have different life cycles and restrictions compared to apps. Avoid heavy tasks in the extension to comply with memory and CPU usage limits.
2. Use only available system methods in extensions to avoid compilation warnings or App Store rejections. Refer to Apple's [Extension Programming Guide](https://developer.apple.com/library/content/documentation/General/Conceptual/ExtensibilityPG/ExtensionOverview.html#//apple_ref/doc/uid/TP40014214-CH2-SW4).
3. Share code between your app and its extension using an embedded framework. Ensure the "Allow app extension API only" box is checked in your framework's project settings.

![Allow Extensions API Only](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9db3c8ef2844cea9/AllowExtensionAPIOnly.png)
