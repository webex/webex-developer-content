---
type: Guide
title: iOS Meetings SDK | Closed Captions
display_title: Closed Captions
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-closed-captions
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-meetings-sdk-closed-captions)

Closed captions offer a text alternative to spoken dialogue, enabling participants in a meeting to read spoken content. This becomes particularly useful in ensuring accessibility and understanding of the content being discussed during a meeting.

---

Each participant in the meeting can independently enable closed captions in the language they want to see the spoken content. In effect, all participants can enable captions in different languages at the same time enabling them to read spoken content in their own native language within same meeting.



> **Info**
>
> Available starting from SDK version 3.10.0.



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

## CaptionItem Details

The `CaptionItem` object holds the caption text, speaker ID, display name, and an `isFinal` flag. The `onCaptionArrived()` method triggers initially with each spoken word (`isFinal=false`). When the speaker pauses or stops, it refines the text for accuracy and context, triggering again with `isFinal=true`. The `isFinal=true` flag indicates that the sentence is complete.

For example the following spoken phrase, "Hello developer, how are you?" can trigger the following callbacks:

1. Callback 1: "hello" -> `isFinal=false`
2. Callback 2: "hello developer" -> `isFinal=false`
3. Callback 3: "hello developer how are" -> `isFinal=false`
4. Callback 4: "hello developer how are you and" -> `isFinal=false` (The word "and" was a false detection.)
5. Callback 5: "hello developer, how are you?" -> `isFinal=true` (If the speaker pauses or stops talking. Normalized statement in terms of context and grammar.)
