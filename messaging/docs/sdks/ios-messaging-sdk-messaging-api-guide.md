---
type: Guide
title: iOS Messaging SDK | Messaging API Guide
display_title: API Guide
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide
content_type: documentation
product_group:
- webex-suite
categories:
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide)

This article provides detailed information on the messaging features and methods provided by the Webex iOS Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Before Continuing: Sync Webex Spaces

Before working with spaces or messages within them, ensure that all spaces are synced using the following method:

```swift
// Indicates if the latest conversations have been synced to the local data warehouse.
// Returns true if the sync is completed.
// Returns false if the sync is in progress.
webex.spaces.isSpacesSyncCompleted 
    
// The callback handler for sync status changes.
webex.spaces.onSyncingSpacesStatusChanged = { isSpacesSyncInProgress in
    // isSpacesSyncInProgress is true if a space sync is in progress.
    // isSpacesSyncInProgress is false if a space sync is complete.
 }
```

![Messaging Flow Diagram](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltadc14f928a4816b3/222117387-a9888f35-be35-4af9-aac7-5c5acf601aef.png)

## Post a Text Message to a Person by ID

To post a text message to a particular participant using their `personId`:

```swift
webex.messages.post(personId: "{personId}", text: "text..."){ response in
     switch response.result {
         case .success(let message):
             // ...
             break
         case let .failure(let error):
             // ...
             break
     }
}
```

### Post a Text Message to a Person by Email

To post a text message to a person using their email address:

```swift
guard let emailAddress = EmailAddress.fromString("{person email address}") else{ return }

webex.messages.post(personEmail: emailAddress, text: "text..."){ response in
     switch response.result {
         case .success(let message):
             // ...
             break
         case let .failure(let error):
             // ...
             break
     }
}
```

### Post a Text Message to a Room

To post a text message to a room using its `roomId`:

```swift
webex.messages.post(roomId: "{roomId}", text: "text..."){ response in
     switch response.result {
         case .success(let message):
             // ...
             break
         case let .failure(let error):
             // ...
             break
     }
}
```

### Post Single Mentions

To post a message that includes mention(s) of individual person(s):

```swift
//create person mention items with personId
let mentionItem1 = Mention.person("{personId1}")
let mentionItem2 = Mention.person("{personId2}")
let mentionArray = [mentionItem1, mentionItem2]

webex.messages.post(roomId: "{roomId}", text: "text...", mentions: mentionArray){ response in
     switch response.result {
         case .success(let message):
             // ...
             break
         case let .failure(let error):
             // ...
             break
     }
}
```

### Post a Group Mention

To post a message that includes a group mention:

```swift
//create a group mention item.
let mentionItem = Mention.all
let mentionArray = [mentionItem]

webex.messages.post(roomId: "{roomId}", text: "text...", mentions: mentionArray){ response in
     switch response.result {
         case .success(let message):
             // ...
             break
         case let .failure(let error):
             // ...
             break
     }
}
```

## Post Local Files

To post a message with attached files using local paths:

```swift
let fileItem1 = LocalFile.init(path: "{local file path}")
let fileItem2 = LocalFile.init(path: "{local file path}", name: "{file name}", mime: "{file mime type}")
let fileArray = [fileItem1, fileItem2]

webex.messages.post(roomId: "{room id}", text: "{text...}", files: fileArray){ response in
    switch response.result {
        case .success(let message):
            // ...
            break
        case let .failure(let error):
            // ...
            break
    }
}
```

### Post Files with Uploading Progress

To post a message with a file and monitor the uploading progress:

```swift
guard let fileItem  = LocalFile.init(path: "{local file path}", name: "{file name}", mime: "{file mime type}", 
    progressHandler: { (progress) in // progress as double }) else {return}

webex.messages.post(roomId: "{room id}", text: "{text...}", files: [fileItem]){ response in
    switch response.result {
        case .success(let message):
            // ...
            break
        case let .failure(let error):
            // ...
            break
    }
}
```

### Post Files with a Thumbnail Preview

To post a message with a file that includes a thumbnail:

```swift
let fileThumb = LocalFile.Thumbnail.init(path: "{file path}", mime: "{mime type}", width: 320, height: 400)
guard let fileItem  = LocalFile.init(path: "{local file path}", name: "{file name}", mime: "{file mime type}", 
    thumbnail: fileThumb, progressHandler: { (progress) in // progress as double }) else {return}

webex.messages.post(roomId: "{room id}", text: "{text...}", files: [fileItem]){ response in
    switch response.result {
        case .success(let message):
            // ...
            break
        case let .failure(let err):
            // ...
            break
    }
}
```

## Delete a Message

To delete a message using its `messageId`:

```swift
webex.messages.delete(messageId: "{message id}", completionHandler: { (response) in
    switch response.result{
        case .success(_):
            // delete operation successful.
            break
        case .failure(let err):
            // delete operation failed
            break
        }
})
```

## List Messages Before a Specific Date

To list messages before a particular date point within a room, with `max` specifying the maximum number of messages to return:

```swift
let before = Before.date("{one date point}")

webex.messages.list(roomId: "{room id}", before: before, max: 50) { response in
    switch response.result {
    case .success(let messages):
        // ...
        break
    case .failure(let err):
        // ...
        break
    }
}
```

## List Messages Before a Specific Message

To list messages before a particular message within a room:

```swift 
let beforeMessage = Before.message("{message id}")

webex.messages.list(roomId: "{room id}", before: beforeMessage, max: 50) { response in
    switch response.result {
    case .success(let messages):
       // ...
       break
    case .failure(let err):
        // ...
        break
     }
}
```

## List Messages That Mentioned Your ID

To list messages in which your ID is mentioned within a group room:

```swift
let mentioned = Mention.person("me")
webex.messages.list(roomId: "{room id}", max: 50, mentionedPeople: mentioned) { response in
    switch response.result {
    case .success(let messages):
        // ...
        break
    case .failure(let err):
        // ...
        break
    }
}
```

## Message Reception Events

To handle message reception events:

```swift
webex.messages.onEvent = { messageEvent in
    switch messageEvent{
    case .messageReceived(let message):
        // received message...
        break
    case .messageDeleted(let messageId):
        // deleted messageId...
        break
    }
}
```

## Download Simple Files

When a message with files is received, this code will download each file to default location:

```swift
webex.messages.onEvent = { messageEvent in
    switch messageEvent{
    case .messageReceived(let message):
        if let files = message.files {
            for file in files {
                webex.messages.downloadFile(file) { result in
                    if let localUrl = result.data{
                        // file downloaded successfully in localUrl ...
                    }
                }
            }
        }
        break
    case .messageDeleted(let messageId):
        // ...
        break
    }
}
```

## Download Files to a Particular Destination

This code snippet is similar to the previous one, but it specifies a destination directory where the files should be downloaded:

```swift
webex.messages.onEvent = { messageEvent in
    switch messageEvent{
    case .messageReceived(let message):
        let destination = URL.init(string: "{destination directory}")
        if let files = message.files {
            for file in files {
               webex.messages.downloadFile(file, to: destination) { result in
                    if let localUrl = result.data{
                       // file downloaded successfully in localUrl ...
                    }
               }
            }
        }
        break
    case .messageDeleted(let messageId):
        // ...
        break
    }
}
```

## Download Files with a Progress Handler

In addition to downloading the files, this snippet provides a progress handler that reports the progress of the file download:

```swift
webex.messages.onEvent = { messageEvent in
    switch messageEvent{
    case .messageReceived(let message):
        if let files = message.files {
            for file in files {
               webex.messages.downloadFile(file, progressHandler: { progress in
                      // progress in double
               }) { result in
                    if let localUrl = result.data{
                      // file downloaded successfully in localUrl ...
                  }
               } 
            }
        }
        break
    case .messageDeleted(let messageId):
        // ...
        break
    }
}
```

## Download Thumbnails

To download the thumbnails of the files included in a message:

```swift
webex.messages.onEvent = { messageEvent in
    switch messageEvent{
    case .messageReceived(let message):
        if let files = message.files {
            for file in files {
                webex.messages.downloadThumbnail(for: file) { result in
                    if let localUrl = result.data{
                        // file downloaded successfully in localUrl ...
                    }
                }
            }
        }
        break
    case .messageDeleted(let messageId):
        // ...
        break
    }
}
```

## Download Thumbnails to a Particular Destination

Similar to downloading files, this snippet specifies a destination for the downloaded thumbnails:

```swift
webex.messages.onEvent = { messageEvent in
    switch messageEvent{
    case .messageReceived(let message):
        let destination = URL.init(string: "{destination directory}")
        if let files = message.files {
            for file in files {
               webex.messages.downloadThumbnail(for: file, to: destination) { result in
                    if let localUrl = result.data{
                       // file downloaded successfully in localUrl ...
                    }
               }
            }
        }
        break
    case .messageDeleted(let messageId):
        // ...
        break
    }
}
```

## Download Thumbnails with a Progress Handler

To download thumbnails with a progress handler to monitor the download progress:

```swift
webex.messages.onEvent = { messageEvent in
    switch messageEvent{
    case .messageReceived(let message):
        if let files = message.files {
            for file in files {
               webex.messages.downloadThumbnail(for: file, progressHandler: { progress in
                      // progress in double
               }) { result in
                    if let localUrl = result.data{
                      // file downloaded successfully in localUrl ...
                  }
               }
            }
        }
        break
    case .messageDeleted(let messageId):
        // ...
        break
    }
}
```

## Send a Read Receipt

To send a read receipt for a message:

```swift
webex.messages.markAsRead(spaceId: spaceId, messageId: messageId, completionHandler: { result in
     switch result {
     case .success(_):
         // Read receipt sent successfully.
     case .failure(let error):
         // Failed to send read receipt.
     }
})
```

## Membership Events

To handle membership change events:

```swift
webex.memberships.onEvent = { membershipEvent in
      switch membershipEvent {
      case .created(let membership):
          // A new membership was created.
      case .deleted(let membership):
          // A membership was deleted.
      case .update(let membership):
          // A membership was updated.
      case .messageSeen(let membership, let lastSeenId):
          // A message was seen by a member.
      }
}
```

## List Memberships with Read Status

To get the read statuses of all memberships in a space:

```swift
webex.memberships.listWithReadStatus(spaceId: spaceId, completionHandler: { response in
      switch response.result {
      case .success(let readStatuses):
          // Process read statuses.
      case .failure(let error):
          // Handle error.
      }
})
```

## Space Events

To handle space change events:

```swift
webex.spaces.onEvent = { spaceEvent in
      switch spaceEvent {
      case .create(let space):
          // A new space was created.
      case .update(let space):
          // A space was updated.
      case .spaceCallStarted(let spaceId):
          // A call started in the space.
      case .spaceCallEnded(let spaceId):
          // A call ended in the space.
      }
}
```

## Get Space Read Status

To get the read status of a space for the logged-in user:

```swift
webex.spaces.getWithReadStatus(spaceId: spaceId, completionHandler: { response in
      switch response.result {
      case .success(let spaceInfo):
          if let lastActivityDate = spaceInfo.lastActivityDate,
              let lastSeenDate = spaceInfo.lastSeenActivityDate,
              lastActivityDate > lastSeenDate {
              // Space has unread messages.
          } else {
              // Space is fully read.
          }
      case .failure(let error):
          // Handle error.
      }
})
```

## Get Space Meeting Info

To get the meeting details of a space:

```swift
webex.spaces.getMeetingInfo(spaceId: spaceId, completionHandler: { result in
      switch result {
      case .success(let meetingInfo):
          // Process meeting info.
      case .failure(let error):
          // Handle error.
      }
})
```

## List Spaces with Active Calls

To get a list of spaces that have an ongoing call:

```swift
webex.spaces.listWithActiveCalls(completionHandler: { result in
    switch result {
    case .success(let spaceIds):
        // Process space IDs with active calls.
    case .failure(_ ):
        // Handle error.
    }
})
```
