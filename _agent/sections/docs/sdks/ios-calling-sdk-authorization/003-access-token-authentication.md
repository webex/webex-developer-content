---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-authorization
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Access Token Authentication
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-authorization). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-authorization.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [OAuth Authentication](001-oauth-authentication.md) [JWT Authentication](002-jwt-authentication.md) [Authentication Event Delegate](004-authentication-event-delegate.md)

## Article introduction

The Webex mobile SDK requires initialization and authorization to interact with the Webex platform. Your app must authenticate users either through an [OAuth](https://oauth.net/) grant flow for Cisco Webex users, or a [JSON Web Token (JWT)](https://developer.webex.com/docs/guest-issuer) for guest users without a Cisco Webex account.

---

This article discusses the methods for authorizing a `Webex` instance.

## Selected section

## Access Token Authentication

Authorize the `Webex` instance using an access token.



> **Info**
>
> For guest users created using the new Service Apps based [Guest Management](https://developer.webex.com/create/docs/sa-guest-management), the generated guest's token should be used with Access Token-based authentication flow.



```swift
let authenticator = TokenAuthenticator(isFedRAMPEnvironment: isFedRAMP)
webex = Webex(authenticator: authenticator)
    authenticator.authorizedWith(accessToken: token, expiryInSeconds: nil, completionHandler: { res in
    if res == .success {
    // Success.
    } else {
    // Failure.
    }
})
```
