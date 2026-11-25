---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-authorization
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- JWT Authentication
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-messaging-sdk-authorization). [Full Markdown](../../../../../docs/sdks/ios-messaging-sdk-authorization.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [OAuth Authentication](001-oauth-authentication.md) [Access Token Authentication](003-access-token-authentication.md) [Authentication Event Delegate](004-authentication-event-delegate.md)

## Article introduction

The Webex mobile SDK requires initialization and authorization to interact with the Webex platform. Your app must authenticate users either through an [OAuth](https://oauth.net/) grant flow for Cisco Webex users, or a [JSON Web Token (JWT)](https://developer.webex.com/docs/guest-issuer) for guest users without a Cisco Webex account.

---

This article discusses the methods for authorizing a `Webex` instance.

## Selected section

## JWT Authentication

Authenticate the `Webex` instance using a JWT for guest users without a `Webex` account:

```swift
let authenticator = JWTAuthenticator()
let webex = Webex(authenticator: authenticator)

webex.initialize { [weak self] isLoggedIn in
    guard let self = self else { return }
    if isLoggedIn {
        print("User is authorized.")
    } else {
        authenticator.authorizedWith(jwt: myJwt) { result in
            switch result {
            case .failure(let error):
                print("JWT login failed.")
            case .success(let authenticated):
                if authenticated {
                    print("JWT login successful.")
                    webex.onInitialSpacesSyncCompleted = {
                        print("Initial space sync succeeded.")
                    }
                }
            }
        }
    }
}
```
