---
type: Guide
title: Android Messaging SDK | Quickstart
display_title: Quickstart
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-quickstart
content_type: documentation
product_group:
- webex-suite
categories:
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-messaging-sdk-quickstart)

This article provides examples of common methods used in the meetings flow for the iOS Messaging SDK. For detailed method parameters, refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/android-sdk-overview#sdk-api-reference).

---

The `Webex` instance is the primary entry point for the SDK, allowing access to all Webex SDK APIs.

## Create a New Webex Space

To create a new Webex space:

```kotlin
webex.spaces.create("Hello World", null, CompletionHandler<Space?> { result ->
    if (result.isSuccessful) {
        val space = result.data
    } else {
        val error= result.error
    }
})
```

## Add a User to a Space

To add a user to a space:

```kotlin
webex.memberships.create(space.id, null, "person@example.com", true, CompletionHandler<Membership?> { result ->
    if (result.isSuccessful) {
        val space = result.data
    } else {
        val error= result.error
    }
})
```

### Post a Message in a Space

To post a message in the space:

```kotlin
webex.messages.postToSpace(space.id, Message.Text.plain("Hello"), null, null, CompletionHandler<Message> { result ->
    if(result != null && result.isSuccessful){
        val message = result.data
    }
})
```

## Post a Message with an Attachment

To post a message to a space with an attachment:

```kotlin

// targetId is the spaceId or personId or email address

webex.messages.post(targetId, Message.draft(Message.Text.markdown("**Hello**", null, null)).addAttachments(localFile), CompletionHandler { result ->
    if (result.isSuccessful) {
        // message sent successfully
    } else {
        val error = result.error
        // message sent failed
    }
})
```

## Post a Message as a Reply to a Thread

To post a message as a reply to a thread:

```kotlin
webex.messages.post(targetId, Message.draft(Message.Text.markdown("**Hello**", null, null))
.addAttachments(localFile)
.setParent(parentMessage),
CompletionHandler { result ->
    if (result.isSuccessful) {
        // message sent successfully
    } else {
        val error = result.error
        // message sent failed
    }
})
```

## Intercept Messaging Events

To intercept messaging events:

```kotlin
webex.messages.setMessageObserver(object : MessageObserver {
    override fun onEvent(event: MessageObserver.MessageEvent) {
        when (event) {
            is MessageObserver.MessageReceived -> {
                val message = event.getMessage()
                if (message?.getParentId() != null) {
                    // Threaded message
                }
            }
            is MessageObserver.MessageDeleted -> {
                // message deleted
            }
            is MessageObserver.MessageFileThumbnailsUpdated -> {
                // thumbnails updated for files
            }
            is MessageObserver.MessageEdited -> {
                // message edited successfully. event.getMessage() returns the edited message.
            }
        }
    }
})
```

## Manage the Background Connection

To maintain a websocket connection in the background (allowing background syncing of messages):

```kotlin
webex.phone.enableBackgroundConnection(enable: Boolean)
```

## Enable or Disable Console Logging

To enable/disable console login:

```kotlin
webex.enableConsoleLogger(enable: Boolean)
```

## Set the Log Level

To set the current log level:

```kotlin
webex.setLogLevel(logLevel: LogLevel)
```

## Check Feature Entitlements for a Logged-In User

To determine what entitlements a particular logged-in user has:

```kotlin
var capability = webex.people.getProductCapability()

var hasCalling = capability.isCallingSupported()
var hasMessaging = capability.isMessagingSupported()
var hasMeeting = capability.isMeetingSupported()
```
