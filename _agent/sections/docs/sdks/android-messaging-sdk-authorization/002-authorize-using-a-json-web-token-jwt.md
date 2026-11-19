---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-authorization
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Authorize Using a JSON Web Token(JWT)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-authorization). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-authorization.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication Event Delegate](005-authentication-event-delegate.md)

## Article introduction

The Webex Mobile Android SDK must be initialized and authorized to interact with the Webex platform. Your application should authenticate users through an [OAuth](https://oauth.net/) grant flow for existing Cisco Webex users or a JSON web token (JWT) for guest users without a Cisco Webex account.

---

This article provides code examples explaining how to perform this authorization using either a built in Webview or an external browser.

## Selected section

## Authorize Using a JSON Web Token(JWT)
`JWTAuthenticator` utilizes a JWT token for user authentication. Create a new `Webex` instance using JWT authentication

```kotlin
val token: String = "jwt_token"
val authenticator: JWTAuthenticator = JWTAuthenticator()
val webex = Webex(application, authenticator)
webex.initialize(CompletionHandler { result ->
    if (result.error == null) {
        // Already authorised
    } else {
        authenticator.authorize(token, CompletionHandler { result ->
                if (result.error != null) {
                    // Handle the error
                }else{
                    // Authorization Successful
                    webex.spaces.setOnInitialSpacesSyncCompletedListener( CompletionHandler { result->
                        if(result.isSuccessful){
                            // Initial Sync successful
                        } 
                    }
                }
            })
    }
})
```
