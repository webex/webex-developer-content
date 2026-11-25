---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream-legacy-support
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Implementing Multistream in SDK 2.8
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream-legacy-support). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-multistream-legacy-support.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides details on how to use multistream features in older versions of the Webex Mobile SDK.

---

However, we highly recommend using the latest Webex Mobile SDKs. Refer to the newer [Multistream](https://developer.webex.com/docs/sdks/android-meetings-sdk-multistream) documentation for the current implementation.

## Selected section

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
