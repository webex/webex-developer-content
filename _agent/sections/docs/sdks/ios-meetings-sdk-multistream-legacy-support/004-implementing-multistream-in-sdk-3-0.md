---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream-legacy-support
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Implementing Multistream in SDK 3.0
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream-legacy-support). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-multistream-legacy-support.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides details on how to use multistream features in older versions of the Webex Mobile SDK.

---

It serves as a reference for legacy implementations, but it is highly recommended to use the latest Webex Mobile SDKs and refer to the newer [Multistream](https://developer.webex.com/docs/sdks/ios-meetings-sdk-multistream) documentation for the current implementations.

![Multistream Example](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8efd63a7f9794b20/multistream.jpeg)

## Selected section

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
