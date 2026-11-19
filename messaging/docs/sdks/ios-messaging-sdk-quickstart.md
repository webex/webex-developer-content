---
type: Guide
title: iOS Messaging SDK | Quickstart
display_title: Quickstart
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-quickstart
content_type: documentation
product_group:
- webex-suite
categories:
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-messaging-sdk-quickstart)

This article provides examples of common methods used in the meetings flow for the iOS Messaging SDK. For detailed method parameters, refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/ios-sdk-overview#sdk-api-reference).

---

The `Webex` instance is the core access point for the SDK, providing access to all Webex SDK methods.

## Create a New Webex Space

To create a new Webex space:

```swift
webex.spaces.create(title: "Hello World") { result in
    switch result {
    case .success(let space):
        // ...
    case .failure(let error):
        // ...
    }
}
```

## Add a User to a Space

To add a user to a space:

```swift
webex.memberships.create(spaceId: spaceId, personEmail: email) { result in    
    switch result {
        case .success(let membership):
            // Handle success
            print("Membership created: \(membership)")
        case .failure(let error):
            // Handle failure
            print("Error creating membership: \(error)")
        }
    }
}
```

### Post a Message in a Space

To post a message in the space:

```swift
webex.messages.post(roomId: "spaceId", text: Message.Text.plain(plain: "hello world")){ response in
    switch result {
        case .success(let message):
            // ...
        case .failure(let error):
            // ...
        }
    }
}
```

## Post a Message with an Attachment

To post a message to a space with an attachment:

```swift
let text = Message.Text.html(html: html)
let thumbnail = LocalFile.Thumbnail(path: thumbnailFilePath, mime: fileType, width: Int(image.size.width), height: Int(image.size.height))

let localFile = LocalFile(path: filePath, name: fileName, mime: fileType, thumbnail: thumbnail, progressHandler: { progress in
                  // Implement progress bar
            })
webex.messages.post(text, toSpace: spaceId, withFiles: localFiles, completionHandler: { response in
    switch response.result {
    case .success(let message):
        // ...
    case .failure(let error):
        // ...
    }
} 
```

## Intercept Messaging Events

To intercept messaging events:

```swift
webex.messages.onEvent = { messageEvent in
    switch messageEvent{
    case .messageReceived(let message):
        // ...
    case .messageDeleted(let messageId):
        // ...
    }
}
```

## Manage the Background Connection

To maintain a websocket connection in the background (allowing background syncing of messages):

```swift
webex.phone.enableBackgroundConnection = true 
```

## Enable or Disable Console Logging

To enable/disable console login:

```swift
webex.enableConsoleLogger = true    
```

## Set the Log Level

To set the current log level:

```swift
webex.logLevel = .verbose 
```

## Check Feature Entitlements for a Logged-In User

To determine what entitlements a particular logged-in user has:

```swift
let capability: ProductCapability = webex.people.getProductCapability()
let hasCalling = capability.isCallingSupported
let hasMeeting = capability.isMeetingSupported
let hasMessaging = capability.isMessagingSupported
```
