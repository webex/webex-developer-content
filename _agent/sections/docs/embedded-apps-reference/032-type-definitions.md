---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-reference
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Type Definitions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-reference). [Full Markdown](../../../../docs/embedded-apps-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

## Type Definitions

The following typed objects are used to represent users, meetings, and spaces.


* [Space](https://developer.webex.com/docs/embedded-apps-api-reference#Space) : object &mdash; Represents a Webex messaging space.
* [User](https://developer.webex.com/docs/embedded-apps-api-reference#User) : object &mdash; Represents a Webex user.



<a name="Space"></a>

### Space

Represents a Space object returned by a call to [ getSpace()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application.Context+getSpace).




**Properties**

- `id` string -- ID of the space (room) in which the app is running. If [app.isPrivateDataAvailable](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+isPrivateDataAvailable) is `true` this property is set to the ID of the Webex space, and can used with the Webex REST APIs. If [app.isPrivateDataAvailable](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+isPrivateDataAvailable) is `false` this property is set to a unique ("derived") value that is guaranteed to be consistent for all app users, but cannot be used with the Webex REST APIs.
- `derivedId` string -- .
- `title` string -- Title of the given space; blank if [app.isPrivateDataAvailable](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+isPrivateDataAvailable) is false.

**Since**: 1.1.0  

* * *


<a name="User"></a>

### User

Represents a User object returned by a call to [ getUser()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application.Context+getUser).




**Properties**

- `id` string -- Webex user ID. If [app.isPrivateDataAvailable](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+isPrivateDataAvailable) is `true` this property contains the user's Webex user ID, and can be used with the Webex REST APIs. If `isPrivateDataAvailable` is `false` this property is set to a unique ("derived") value that is guaranteed to be consistent for the same user and app, but cannot be used with the Webex REST APIs.
- `orgId` string -- Organization ID. If [app.isPrivateDataAvailable](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+isPrivateDataAvailable) is `true` this property is set to the ID of the user's Webex organization, and can be used with the Webex REST APIs. If `isPrivateDataAvailable` is `false` this property is set to a unique ("derived") value that is guaranteed to be consistent for the same combination of user, organization, and app, but cannot be used with Webex APIs.
- `email` string -- Webex user's registered email, or an empty string iff [app.isPrivateDataAvailable](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+isPrivateDataAvailable) is `false`.
- `displayName` string -- Webex user's display name, or an empty string if [app.isPrivateDataAvailable](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+isPrivateDataAvailable) is false.
- `token` string -- [JSON Web Token](https://developer.webex.com/docs/embedded-apps-guide#about-the-json-web-token) (JWT) generated for the user by the Webex identity service.

**Since**: 1.1.0  

* * *
