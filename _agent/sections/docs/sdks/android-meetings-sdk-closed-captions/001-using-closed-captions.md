---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-closed-captions
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Using Closed Captions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-closed-captions). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-closed-captions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Closed captions offer a text alternative to spoken dialogue, enabling participants in a meeting to read spoken content. This becomes particularly useful in ensuring accessibility and understanding of the content being discussed during a meeting.

---

Each participant in the meeting can independently enable closed captions in the language they want to see the spoken content. In effect, all participants can enable captions in different languages at the same time enabling them to read spoken content in their own native language within same meeting.



> **Info**
>
> Available starting from SDK version 3.10.0.

## Selected section

## Using Closed Captions

To use the closed caption functionality of the Android Meetings SDK:

### 1. Check if Closed Captions are allowed

Before using closed captions during a meeting, ensure they are allowed in the meeting in progress to avoid any issues:

```kotlin
var isAllowed = call.isClosedCaptionAllowed
```

### 2. Check if Closed Captions are enabled

Check if closed captions are enabled for the current meeting:

```kotlin
var isEnabled = call.isClosedCaptionEnabled
```

### 3. Toggle Closed Captions

Use a toggle to turn closed captions on or off during a meeting. The `CompletionHandler` indicates if the operation was successful or not.

You should rely on the `onClosedCaptionsInfoChanged` callback when captions are enabled to get the latest information updates:

```kotlin
call?.toggleClosedCaption(enable) {
    if (it.isSuccessful) {
        // captions toggled successfully
    } else {
        // toggle failed
    }
}
```

### 4. Observe Closed Captions Info Changes

To get the latest Closed Captions info for current spoken language and translation language, implement a `CallObserverInterface.onClosedCaptionsInfoChanged()` callback. Make captions are allowed and enabled:

```kotlin
call?.setObserver(object : CallObserver {
    override fun onClosedCaptionsInfoChanged(closedCaptionsInfo: ClosedCaptionsInfo) {
        // Use this callback to update UI for Spoken or Translation language
    }
})
```

### 5. Retrieve Closed Caption Information

Use the `getClosedCaptionsInfo` method to retrieve the closed captions info object, which contains information such as the current spoken and translation languages. Captions need to be enabled to use this method:

```kotlin
val ccInfo = call?.getClosedCaptionsInfo()
```

### 6. Set the Spoken Language

In instances that require a change in the spoken language, use the `setSpokenLanguage()` method. However, it's crucial to note that only the host can change the spoken language to ensure controlled communication flow:

```kotlin
call?.setSpokenLanguage(languageItem.code ) {
    if (it.isSuccessful) {
        // spoken language changed successfully
    }
}
```

### 7. Set the Translation Language

Use the `setTranslationLanguage` method to change the language of closed captions. This method specifies the language in which the text is displayed to the application:

```kotlin
call?.setTranslationLanguage(languageItem.code ) {
    if (it.isSuccessful) {
        // translation language changed successfully
    }
}
```

### 8. Access All Received Closed Captions

Retrieve a complete list of all closed captions from the start of the meeting to the present, allowing users to view previous captions:

```kotlin
val captionItems = call?.getClosedCaptions()
```

### 9. Manage Incoming Closed Captions

Implement a `CallObserverInterface.onClosedCaptionsArrived()` callback to manage and show new Closed Captions as they arrive during a meeting:

```kotlin
call?.setObserver(object : CallObserver {
    override fun onClosedCaptionsArrived(captions: CaptionItem) {
        // Show your captions here
    }
})
```
