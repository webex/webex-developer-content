---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-closed-captions
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Using Closed Captions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-closed-captions). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-closed-captions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Closed captions offer a text alternative to spoken dialogue, enabling participants in a meeting to read spoken content. This becomes particularly useful in ensuring accessibility and understanding of the content being discussed during a meeting.

---

Each participant in the meeting can independently enable closed captions in the language they want to see the spoken content. In effect, all participants can enable captions in different languages at the same time enabling them to read spoken content in their own native language within same meeting.



> **Info**
>
> Available starting from SDK version 3.10.0.

## Selected section

## Using Closed Captions

To use the closed caption functionality of the iOS Meetings SDK:

### 1. Check if Closed Captions are allowed

Before using closed captions during a meeting, ensure they are allowed in the meeting in progress to avoid any issues:

```swift
var isAllowed = call.isClosedCaptionAllowed 
```

### 2. Check if Closed Captions are enabled

Check if closed captions are enabled for the current meeting:

```swift
var isEnabled = call.isClosedCaptionEnabled 
```

### 3. Toggle Closed Captions

Use a toggle to turn closed captions on or off during a meeting. The `CompletionHandler` indicates if the operation was successful or not.

You should rely on the `onClosedCaptionsInfoChanged` callback when captions are enabled to get the latest information updates.

```swift
call.toggleClosedCaption(enable: Bool, completionHandler: { isOn in
    print("Setting toggleClosedCaption to: \(enable), operation returned: \(isOn)")
}) 
```

### 4. Observing Closed Captions info changes

To get the latest closed captions information for the current spoken language and translation language, register a listener on an active call. Ensure that captions are allowed and enabled:

```swift
call.onClosedCaptionsInfoChanged = { info in
    print(info.canChangeSpokenLanguage)
    print(info.currentSpokenLanguage)
    print(info.currentTranslationLanguage)
    print(info.spokenLanguages)
    print(info.translationLanguages)
} 
```

### 5. Retrieve Closed Caption Information

Use the `getClosedCaptionsInfo` method to retrieve the closed captions info object, which contains information such as the current spoken and translation languages. Captions need to be enabled to use this method:

```swift
let ccInfo = call.getClosedCaptionsInfo 
```

### 6. Set the Spoken Language

In instances that require a change in the spoken language, use the `setCurrentSpokenLanguage()` method. However, it's crucial to note that only the host can change the spoken language to ensure controlled communication flow:

```swift
let ccInfo = call.setCurrentSpokenLanguage(language: LanguageItem, completionHandler: {
    error in
    print(error)
}) 
```

### 7. Set the Translation Language

Use the `setCurrentTranslationLanguage` method to change the language of closed captions. This method specifies the language in which the text is displayed to the application:

```swift
let ccInfo = call.setCurrentTranslationLanguage(language: LanguageItem, completionHandler: {
    error in
    print(error)
}) 
```

### 8. Access All Received Closed Captions

Retrieve a complete list of all closed captions from the start of the meeting to the present, allowing users to view previous captions:

```swift
let captionItems = call.getClosedCaptions() 
```

### 9. Manage Incoming Closed Captions

Set up a listener to manage and show new closed captions as they arrive during a call:

```swift
call.onClosedCaptionArrived = { caption in
    // Implementation details...
} 
```
