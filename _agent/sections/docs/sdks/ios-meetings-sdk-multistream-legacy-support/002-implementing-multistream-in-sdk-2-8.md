---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream-legacy-support
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Implementing Multistream in SDK 2.8
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream-legacy-support). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-multistream-legacy-support.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides details on how to use multistream features in older versions of the Webex Mobile SDK.

---

It serves as a reference for legacy implementations, but it is highly recommended to use the latest Webex Mobile SDKs and refer to the newer [Multistream](https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream) documentation for the current implementations.

![Multistream Example](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8efd63a7f9794b20/multistream.jpeg)

## Selected section

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
