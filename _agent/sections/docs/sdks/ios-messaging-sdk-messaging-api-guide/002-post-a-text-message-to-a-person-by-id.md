---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Post a Text Message to a Person by ID
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-messaging-sdk-messaging-api-guide). [Full Markdown](../../../../../docs/sdks/ios-messaging-sdk-messaging-api-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex iOS Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

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
