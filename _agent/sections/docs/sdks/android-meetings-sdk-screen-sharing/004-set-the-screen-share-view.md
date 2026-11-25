---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-screen-sharing
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Set the Screen Share View
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-screen-sharing). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-screen-sharing.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex iOS Meetings SDK allows you to share the entire screen of your Android mobile device during a call or meeting.

---

This article guides your through implementing screen sharing in your own Android application.

## Selected section

## Set the Screen Share View

To view screen or content shared by a remote participant, create a [`MediaOption`](https://ciscospark.github.io/spark-android-sdk/com/ciscospark/androidsdk/phone/MediaOption.html) with the `audioVideoShare` function for the `dial` or `answer` method:

```java
MediaOption option = MediaOption. audioVideoSharing(new Pair<>(localView, remoteView),shareView);

webex.phone().dial("coworker@acm.com", option, (result) -> {
            if (result.isSuccessful()) {
                call = result.getData();
                call.setObserver(callObserver);
            }
            //...
});
```

You can also provide a view only at the point when the other party starts sharing their screen:

```java
MediaOption option = MediaOption. audioVideoSharing(new Pair<>(localView, remoteView),null);

webex.phone().dial("coworker@acm.com", option, (result) -> {
    if (result.isSuccessful()) {
        call = result.getData();
        call.setObserver(callObserver);
    }
    //...
});


@Override
public void onMediaChanged(MediaChangedEvent mediaChangedEvent) {
    if (mediaChangedEvent instanceof RemoteSendingSharingEvent) {
        if (((RemoteSendingSharingEvent) mediaChangedEvent).isSending()) {
            mediaChangedEvent.getCall().setSharingRenderView(shareView);
        } else if (!((RemoteSendingSharingEvent) mediaChangedEvent).isSending()) {
            mediaChangedEvent.getCall().setSharingRenderView(null);
        }
    }
}
```
