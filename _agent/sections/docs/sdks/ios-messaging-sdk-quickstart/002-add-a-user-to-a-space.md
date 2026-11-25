---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-quickstart
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Add a User to a Space
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-messaging-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/ios-messaging-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides examples of common methods used in the meetings flow for the iOS Messaging SDK. For detailed method parameters, refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/ios-sdk-overview#sdk-api-reference).

---

The `Webex` instance is the core access point for the SDK, providing access to all Webex SDK methods.

## Selected section

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
