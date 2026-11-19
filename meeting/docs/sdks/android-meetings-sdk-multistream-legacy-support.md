---
type: Guide
title: Android Meetings SDK | Multistream Legacy Support
display_title: Multistream Legacy Support
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream-legacy-support
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream-legacy-support)

This article provides details on how to use multistream features in older versions of the Webex Mobile SDK.

---

However, we highly recommend using the latest Webex Mobile SDKs. Refer to the newer [Multistream](https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream) documentation for the current implementation.

## Multistream in SDK 2.8 Using Aux Streams

Multistream allows participants to see the video of the most active speakers in a meeting. Each video stream is known as an auxiliary stream. Auxiliary streams can display active participants, with the primary active speaker shown on the main remote video view and other active speakers on auxiliary video views.

![Multistream-example](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt76accc9a83783b10/Screenshot_20180907-164030.png)

### Typical Scenario in SDK 2.8

In meetings with more than two participants, use multistream to view the active speaker and other participants.

### Limitations in SDK 2.8

Please be aware of the following limitations:

- A maximum of 4 auxiliary video streams are allowed.
- The stream for a specific participant is based on activity, not selection.

## Implementing Multistream in SDK 2.8

To use multi-stream, implement the `MultiStreamObserver` interface:

```java
public interface MultiStreamObserver {
    View onAuxStreamAvailable();
    View onAuxStreamUnavailable();
    void onAuxStreamChanged(AuxStreamChangedEvent event);
}
```

### Provide a View for an Auxiliary Stream

When a new auxiliary stream is available, the SDK calls `onAuxStreamAvailable` and the client provides a view for rendering. The `AuxStreamOpenedEvent` indicates if the stream opened successfully:

```java
@Override
public View onAuxStreamAvailable() {
    // SDK will open this auxiliary stream with this view and the result will be notified by AuxStreamOpenedEvent.
    View auxStreamView = LayoutInflater.from(getActivity()).inflate(R.layout.remote_video_view, null);
    AuxStreamViewHolder auxStreamViewHolder = new AuxStreamViewHolder(auxStreamView);
    mAuxStreamViewMap.put(auxStreamViewHolder.mediaRenderView, auxStreamViewHolder);
    return auxStreamViewHolder.mediaRenderView;
}
```

### Close an Auxiliary Stream

When an auxiliary stream is unavailable, the SDK calls `onAuxStreamUnavailable`. The client can then provide a view to be closed or allow the SDK to close the last opened stream:

```java
@Override
public View onAuxStreamUnavailable() {
    // You can close a view or let the SDK automatically close the last opened view.
    // The result will be signalled by a AuxStreamClosedEvent.
    return null;
}
```

### Display an Auxiliary Stream

Handle the `AuxStreamOpenedEvent` to display the auxiliary stream view if it is successfully opened.

### Hide an Auxiliary Stream

Handle the `AuxStreamClosedEvent` to hide the auxiliary stream view when it is successfully closed:

```java
@Override
public void onAuxStreamChanged(AuxStreamChangedEvent event) {
    if (event instanceof MultiStreamObserver.AuxStreamOpenedEvent) {
        if ((AuxStreamOpenedEvent)event.isSuccessful()){
            Ln.d("AuxStreamOpenedEvent successful");
            viewAuxVideos.addView(mAuxStreamViewMap.get((AuxStreamOpenedEvent)event.getRenderView()).item);
        }else{
            Ln.d("AuxStreamOpenedEvent failed: " + (AuxStreamOpenedEvent)event.getError());
            mAuxStreamViewMap.remove((AuxStreamOpenedEvent)event.getRenderView());
        }
    } else if (event instanceof MultiStreamObserver.AuxStreamClosedEvent) {
        if ((AuxStreamClosedEvent)event.isSuccessful()){
            Ln.d("AuxStreamClosedEvent successful");
            AuxStreamViewHolder auxStreamViewHolder = mAuxStreamViewMap.get((AuxStreamClosedEvent)event.getRenderView());
            mAuxStreamViewMap.remove((AuxStreamClosedEvent)event.getRenderView());
            viewAuxVideos.removeView(auxStreamViewHolder.item);
        }else{
            Ln.d("AuxStreamClosedEvent failed: " + (AuxStreamClosedEvent)event.getError());
        }
    } 
}
```

## Multistream in SDK 3.0 Using Aux Streams

Multistream displays the video of the most active participants. Streams are allocated based on the order of joining, and participants exceeding the limit are placed in a queue. Active speakers can take over streams, and when participants leave, others from the queue will replace them.

![Multistream example](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4e03685952149e13/multistream.png)

### Limitations in SDK 3.0

Please be aware of the following limitations:

- A maximum of 4 auxiliary video streams are allowed.
- The stream for a specific participant is based on activity, not selection.

## Implementing Multistream in SDK 3.0

To implement multi-stream in SDK 3.0, inherit from `MultiStreamObserver`:

```kotlin
interface MultiStreamObserver {
    fun onAuxStreamAvailable(): View?
    fun onAuxStreamUnavailable(): View?
    fun onAuxStreamChanged(event: AuxStreamChangedEvent?)
}
```

### Provide a View to Open a Stream

When a new stream is available, the `onAuxStreamAvailable` method is called. The client provides a view to render the stream:

```kotlin
override fun onAuxStreamAvailable(): View? {
    return mediaRenderView
}
```

### Provide a View to Close the Stream

If a stream is unavailable, such as when a participant leaves the meeting and the number of joined participants is smaller than the number of opened streams, the SDK will trigger the `OnAuxStreamUnavailable` callback. The client should provide the SDK with a view handle to be closed. If the given view is null, the SDK will automatically close the last opened stream if needed:

```kotlin
override fun onAuxStreamUnavailable(): View? {
    return null
}
```

### Display the Stream View

Handle the `AuxStreamOpenedEvent` to display the stream view when it is successfully opened.

### Hide the Stream View

Handle the `AuxStreamClosedEvent` to hide the stream view when it is successfully closed:

```kotlin
override fun onAuxStreamChanged(event: MultiStreamObserver.AuxStreamChangedEvent?) {
    val auxStream: AuxStream? = event?.getAuxStream()

    when (event) {
        is MultiStreamObserver.AuxStreamOpenedEvent -> {
            if (event.isSuccessful()) {
                ...
            } else {
                // error occurred
            }
        }
        is MultiStreamObserver.AuxStreamClosedEvent -> {
            if (event.isSuccessful()) {
                ...
            } else {
                // error occurred
            }
        }
        is MultiStreamObserver.AuxStreamSendingVideoEvent -> {
            ...     
        }
        is MultiStreamObserver.AuxStreamPersonChangedEvent -> {
            ...
        }
        is MultiStreamObserver.AuxStreamSizeChangedEvent -> {
            ...
        }
    }
}
```
