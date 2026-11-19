---
type: Guide
title: iOS Meetings SDK | Multistream Legacy Support
display_title: Multistream Legacy Support
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream-legacy-support
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream-legacy-support)

This article provides details on how to use multistream features in older versions of the Webex Mobile SDK.

---

It serves as a reference for legacy implementations, but it is highly recommended to use the latest Webex Mobile SDKs and refer to the newer [Multistream](https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream) documentation for the current implementations.

![Multistream Example](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8efd63a7f9794b20/multistream.jpeg)

## Multistream in SDK 2.8 Using Aux Streams

Multistream allows participants to see the video of the most active speakers in a meeting. Each video stream is known as an auxiliary stream. Auxiliary streams can display active participants, with the primary active speaker shown on the main remote video view and other active speakers on auxiliary video views.

![Image described in the surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5e2690071b433887/IMG_0910.jpg)

### Typical Scenario in SDK 2.8

In meetings with more than two participants, use multistream to view the active speaker and other participants.

### Limitations in SDK 2.8

Please be aware of the following limitations:

- A maximum of 4 auxiliary video streams are allowed.
- The stream for a specific participant is based on activity, not selection.

## Implementing Multistream in SDK 2.8

Implement the `MultiStreamObserver` protocol to use multistream:

```swift
class MyVideoCallViewController: UIViewController,MultiStreamObserver {
    var onAuxStreamAvailable: (()-> MediaRenderView?)?
    var onAuxStreamChanged: ((AuxStreamChangeEvent) -> Void)?
    var onAuxStreamUnavailable: (() -> MediaRenderView?)?

    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        self.call.multiStreamObserver = self
    }
}
```

### Provide a View for an Auxiliary Stream

When a new auxiliary stream becomes available, `onAuxStreamAvailable` is called. Provide a view for video rendering:

```swift
var onAuxStreamAvailable: (() -> MediaRenderView?)? = {
    // Callback when a new multistream media is available. Return a `MediaRenderView` to let the SDK open it automatically.
    return self.auxiliaryStreamUI.filter({$0.notInUse}).first?.mediaRenderView
}
```

### Close an Auxiliary Stream

`onAuxStreamUnavailable` is invoked when an auxiliary stream is no longer available. The client provides a view to be closed or lets the SDK close the last opened stream:

```swift
var onAuxStreamUnavailable: (() -> MediaRenderView?)? = {
   return self.auxiliaryStreamUI.filter({$0.inUse}).last?.mediaRenderView
}
```

### Display an Auxiliary Stream

Handle the `auxStreamOpenedEvent` to display the auxiliary stream view upon successful opening.

### Hide an Auxiliary Stream

Handle the `auxStreamClosedEvent` to hide the auxiliary stream view upon successful closure:

```swift
var onAuxStreamChanged: ((AuxStreamChangeEvent) -> Void)? = { event in
    switch event {
        // Callback for open an auxiliary stream results.
        case .auxStreamOpenedEvent(let view, let result):
            switch result {
                case .success(let auxStream):
                    self.updateAuxiliaryUIBy(auxStream: auxStream)
                case .failure(let error):
                    print("========\(error)=====")
            }
         // Triggered when the auxiliary stream's speaker has changed.
         case .auxStreamPersonChangedEvent(let auxStream,_,_):
             self.updateAuxiliaryUIBy(auxStream: auxStream)
         // Triggered when the speaker muted or unmuted the video.
         case .auxStreamSendingVideoEvent(let auxStream):
             self.updateAuxiliaryUIBy(auxStream: auxStream)
         // Triggered when the speaker's video rendering view size has changed.
         case .auxStreamSizeChangedEvent(let auxStream):
             self.updateAuxiliaryUIBy(auxStream: auxStream)
         // Callback to close an auxiliary stream.
         case .auxStreamClosedEvent(let view, let error):
             if error == nil {
                 self.closedAuxiliaryUI(view: view)
             } else {
                 print("=====auxStreamClosedEvent error:\(String(describing: error))")
             }
     }
}
```

## Multistream in SDK 3.0 Using Aux Streams

Multistream lets you view multiple active participants in a meeting:

- Stream order is based on the order of joining.
- Beyond 6 participants (self, remote, and auxiliary streams), extra participants queue up and aren't allocated streams.
- Active participants from the queue replace less active streams.
- Departing participants' streams are replaced by queued participants.
- Use the [Active Speaker Method](https://webex.github.io/webex-ios-sdk/Structs/CallMembership.html#/s:8WebexSDK14CallMembershipV15isActiveSpeakerSbvp) to identify the active speaker.
- The [ActiveSpeakerChangedEvent](https://webex.github.io/webex-ios-sdk/Classes/Call/MediaChangedEvent.html#/s:8WebexSDK4CallC17MediaChangedEventO013activeSpeakereF0yAeA0C10MembershipVSg_AItcAEmF) triggers when the active speaker changes.

### Typical Scenario in SDK 3.0

Use multistream in meetings with more than two participants to view the active speaker and others.

### Limitations in SDK 3.0

- You can display a maximum of 4 streams.
- Specific participant streams cannot be chosen; activity determines allocation.

## Implementing Multistream in SDK 3.0

Inherit and implement the `MultiStreamObserver` interface as follows:

```swift
class ViewController: UIViewController, MultiStreamObserver {
    var onAuxStreamAvailable: (()-> MediaRenderView?)?
    var onAuxStreamChanged: ((AuxStreamChangeEvent) -> Void)?
    var onAuxStreamUnavailable: (() -> MediaRenderView?)?

    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        self.call.multiStreamObserver = self
    }
}
```

### Provide a View to Open a Stream

When a new stream is available, `onAuxStreamAvailable` is called. The client provides a view to render the stream.

```swift
var onAuxStreamAvailable: (() -> MediaRenderView?)? = { 
    }
```

### Provide a View to Close the Stream

If a stream becomes unavailable, such as when a participant leaves the meeting and the number of joined participants is smaller than the number of opened streams, the SDK triggers the `onAuxStreamUnavailable` callback. The client should provide the SDK with a view handle to be closed. If the provided view is null, the SDK automatically closes the last opened stream if needed:

```swift
var onAuxStreamUnavailable: (() -> MediaRenderView?)? = {
   }
```

### Display the Stream View

Handle the `AuxStreamOpenedEvent` to display the stream view upon successful opening.

### Hide the Stream View

Handle the `AuxStreamClosedEvent` to hide the stream view upon successful closure:

```swift
 var onAuxStreamChanged: ((AuxStreamChangeEvent) -> Void)? = { event in
            switch event {
                
                case .auxStreamOpenedEvent(let view, let result):
                    switch result {
                    case .success(let auxStream):
                    // Perform actions with auxStream.
                    case .failure(let error):

                    @unknown default:
                        break
                    }

                case .auxStreamPersonChangedEvent(let auxStream, let old, let new):
                
                case .auxStreamSendingVideoEvent(let auxStream):
                
                case .auxStreamSizeChangedEvent(let auxStream):
                
                case .auxStreamClosedEvent(let view, let error):
                    if error == nil {
                     // Perform actions when the stream closes successfully.
                    } else {

                    }
                @unknown default:
                    break
            }
        }
```
