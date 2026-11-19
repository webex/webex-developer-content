---
type: Guide
title: Android Messaging SDK | Features and Methods
display_title: Features and Methods
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods
content_type: documentation
product_group:
- webex-suite
categories:
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods)

This article provides detailed information on the messaging features and methods provided by the Webex Android Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Before Continuing: Sync Webex Spaces

Before working with spaces or messages within them, ensure that all spaces are synced using the following method:

```kotlin
// Indicates if the latest conversations have been synced to the local data warehouse.
// Returns true if the sync is completed.
// Returns false if the sync is in progress.
webex.spaces.isSpacesSyncCompleted 
    
// The callback handler for sync status changes.
webex.spaces.setOnSpaceSyncingStatusChangedListener( CompletionHandler { result->
    if(result.isSuccessful){
        // result.data provides the sync status.
        if(result.data){
        // result.data is true if a spaces sync is in progress.
        }
        else{
        // result.data is false if a spaces sync is complete.
        }
    }
}
```

![Messaging Flow Diagram](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5714a922c6bed71b/messaging-sequence.png)

## Get a Message by ID

Retrieve a specific message using its ID:

```kotlin
webex.messages.get(messageId, CompletionHandler { result ->
    if (result.isSuccessful) {
        // result.data gives the message object
    } else {
        // result.error?.errorMessage gives error message
    }
})
```

## Send a Text Message

Send a text messages to a person via ID or email, or to a space:

```kotlin
webex.messages.postToPerson(personId, message, null, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Success. result.data contains the Message object
    } else {
        // Error occurred. result.error?.errorMessage provides the error message
    }
})
```

```kotlin
val emailAddress = EmailAddress.fromString(email) // email is the Email address in string format
webex.messages.postToPerson(emailAddress, message, files, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Success. result.data contains the Message object
    } else {
        // Error occurred. result.error?.errorMessage provides the error message
    }
})
```

```kotlin
val text: Message.Text = Message.Text.plain("some_message")
webex.messages.postToSpace(spaceId, text, null, null, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Success. result.data contains the Message object
    } else {
        // Error occurred. result.error?.errorMessage provides the error message
    }
})
```

## Post a Message to a Space or a Person using a Draft object

The `target` is the destination to which the message is being sent and can be a person ID, space ID, or email address. The `draft` is of type [Message.Draft](https://webex.github.io/webex-android-sdk/-s-d-k/com.ciscowebex.androidsdk.message/-message/-draft/index.html?query=interface%20Draft).

To post a message to a space or person using a draft object:

```kotlin
webex.messages.post(target, draft, CompletionHandler { result ->
    if (result.isSuccessful) {
        // result.data contains the message object
    } else {
        // result.error?.errorMessage gives the error message
    }
})
```

## Post Mentions

To post a message mentioning a particular person using a person ID:

```kotlin
// Mention individuals
val mentionsList = ArrayList<Mention>()
mentionsList.add(Mention.Person("personId1", startIndex, endIndex))
mentionsList.add(Mention.Person("personId2", startIndex, endIndex))
webex.messages.postToSpace(spaceId, text, mentionsList, files, completionHandler)
```

To post a mention to a group:

```kotlin
// Mention groups
val mentionsList = ArrayList<Mention>()
mentionsList.add(Mention.All())
webex.messages.postToSpace(spaceId, text, mentionsList, files, completionHandler)
```



> **Info**
>
> The `startIndex` and `endIndex` are the index positions in the text message which will indicate the mention object. For example, to mention **XYZ** in the text `Hello XYZ`, the index position would be 6 and 8, where 6 is the `startIndex` and 8 is the `endIndex`.



## Post Files and Track Upload Progress

To attach files to messages:

```kotlin
// Attach files to a message
val text = Message.Text.plain("hello world")
// Create a File object
val tempFile = File.createTempFile("tempFile", ".txt")
// Create a local file object
val localFile = LocalFile(tempFile, "text/html", null, null)
val listOfFiles = ArrayList<LocalFile>()
listOfFiles.add(localFile)
webex.messages.postToSpace(spaceId, text, mentionsList, listOfFiles, completionHandler)
```

To track the file upload progress:

```kotlin
// Track upload progress

val text = Message.Text.plain("hello world")
// Create a File object
val tempFile = File.createTempFile("tempFile", ".txt")
// Create a local file object
val localFile = LocalFile(tempFile, "text/html", null, object : MessageClient.ProgressHandler {
    override fun onProgress(bytes: Double) {
        // Use the bytes value to denote quantity uploaded
    }
})
val listOfFiles = ArrayList<LocalFile>()
listOfFiles.add(localFile)
webex.messages.postToSpace(spaceId, text, mentionsList, listOfFiles, completionHandler)
```

## Attach Files with Thumbnails

To attach a file with a thumbnail:

```kotlin
// Attach files with a thumbnail
// Create a File object
val file = File.createTempFile("tempFile", ".txt")
// Create a thumbnail
var thumbnail = LocalFile.Thumbnail(file, null, 320, 400)
// Create a local file object
val localFile = LocalFile(file, "text/html", thumbnail, object : MessageClient.ProgressHandler {
    override fun onProgress(bytes: Double) {
        // Use the bytes value to denote quantity uploaded
    }
})
val listOfFiles = ArrayList<LocalFile>()
listOfFiles.add(localFile)
webex.messages.postToSpace(spaceId, text, mentionsList, listOfFiles, completionHandler)
```

## Edit a Message

To modify the content of an existing message:

```kotlin
webex.messages.edit(messageObject, text, mentions, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Edit success
        val newMessageObject = result.data
    } else {
        // Error occurred. result.error?.errorMessage provides the error message
    }
})
```

## Delete a Message

To delete a message using it message ID:

```kotlin
webex.messages.delete(messageId, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Message deleted successfully
    } else {
        // Error occurred. result.error?.errorMessage provides the error message
    }
})
```

## List Messages Before a Specific Date

To retrieve messages in a space before a given date:

```kotlin
val before = Before.Date(date)
webex.messages.list(spaceId, before, max, mentions, { result ->
    if (result.isSuccessful) {
        // result.data contains the messages
    } else {
        // Error occurred. result.error?.errorMessage provides the error message
    }
})
```



> **Info**
>
> Specify the maximum number of messages to return using `max`.



## List Messages Before a Specific Message

To retrieve messages in a space preceding a certain message ID:

```kotlin
val before = Before.Message("messageId")
webex.messages.list(spaceId, before, max, mentions, { result ->
    if (result.isSuccessful) {
        // result.data contains the messages
    } else {
        // Error occurred. result.error?.errorMessage provides the error message
    }
})
```



> **Info**
>
> Specify the maximum number of messages to return using `max`.



## List Messages Mentioning a Specific Person

To list messages mentioning a particular person, identified by `personId`, in a space:

```kotlin 
val mentionsList : ArrayList<Mention> = ArrayList()
mentionsList.add(Mention.Person(personIdOfSomePersonInSpace))
mentionsList.add(Mention.Person(personIdOfAnotherPersonInSpace))
webex.messages.list(spaceId, null, max, mentionsList, { result ->
    if (result.isSuccessful) {
        // result.data contains the messages
    } else {
        // Error occurred. result.error?.errorMessage provides the error message
    }
})
```


> **Info**
>
> Specify the maximum number of messages to return using `max`.



## Set Up a Message Observer

To set up a message observer to receive messaging events:

```kotlin
webex.messages.setMessageObserver(object : MessageObserver {
    override fun onEvent(event: MessageObserver.MessageEvent) {
        when (event) {
            is MessageObserver.MessageReceived -> {
                // event.getMessage() gives the Message object
            }
            is MessageObserver.MessageDeleted -> {
                ...
            }
            is MessageObserver.MessageFileThumbnailsUpdated -> {
                ...
            }
            is MessageObserver.MessageEdited -> {
                ...
            }
            is MessageObserver.MessagesUpdated -> {
                ...
            }
        }
    }
})
```

## Download Files from a Message

Download files included in a message to a specified local directory where `file` includes the directory and file name:

```kotlin
webex.messages.downloadFile(remoteFile, file,
    object : MessageClient.ProgressHandler {
        override fun onProgress(bytes: Double) {
        }
    },
    CompletionHandler { fileUrlResult ->
        if (fileUrlResult.isSuccessful) {
            // Download successful. fileUrlResult.data gives the file URI
        } else {
            // Error occurred. fileUrlResult.error?.errorMessage gives the error message
        }
    }
)
```



> **Info**
>
> The `remoteFile` is the target file and is of type [Remote File](https://webex.github.io/webex-android-sdk/-s-d-k/com.ciscowebex.androidsdk.message/-remote-file/index.html?query=interface%20RemoteFile).



## Download Thumbnail Images

To download thumbnail images associated with a `RemoteFile` object:

`file` is the local file directory in which the thumbnail is to be saved.
```kotlin
webex.messages.downloadThumbnail(remoteFile, file, CompletionHandler { result ->
    if (result.isSuccessful) {
        if (result.data != null) {
            // result.data gives the thumbnail URI
        } else {
            // Error occurred
        }
    } else {
        emitter.onError(Throwable(result.error?.errorMessage))
    }
})
```



> **Info**
>
> The `remoteFile` is the target file and is of type [Remote File](https://webex.github.io/webex-android-sdk/-s-d-k/com.ciscowebex.androidsdk.message/-remote-file/index.html?query=interface%20RemoteFile).



## Mark a Specific Message as Read

To mark all messages sent before and including the specified `messageId` in a space as read:

```kotlin
webex.messages.markAsRead(spaceId, messageId, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Message is marked as read
    } else {
        // result.error?.errorMessage gives the error message
    }
})
```

## Mark All Messages as Read

To mark **ALL** the messages in a space as read:

```kotlin
 webex.messages.markAsRead(spaceId)
```

## Retrieve the Last Read Message Status

To obtain the last activity and read status in a space:

 ```kotlin
 webex.spaces.getWithReadStatus(spaceId, CompletionHandler { result ->
    if (result.isSuccessful) {
        //show the data
    } else {
        //handle error
    }
})
```

## List Spaces with Active Calls

To get a list of spaces that currently have an ongoing call:

```kotlin
webex.spaces.listWithActiveCalls(CompletionHandler { result ->
    if (result.isSuccessful) {
        // callback returned success, result.data gives data if any
    } else {
        // callback returned failure
    }
})
```

### Check for 'All' Mentions in a Message

To determine if a message mentions all participants in a space:

```kotlin
message.isAllMentioned()
```

### Retrieve a List of Mentioned People in a Message

To retrieve a list of people mentioned in a message:

```kotlin
var mentions = message.getMentions()
```
