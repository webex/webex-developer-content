---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-authorization
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Authorize Using an External Browser
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-authorization). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-authorization.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication Event Delegate](005-authentication-event-delegate.md)

## Article introduction

The Webex Mobile Android SDK must be initialized and authorized to interact with the Webex platform. Your application should authenticate users through an [OAuth](https://oauth.net/) grant flow for existing Cisco Webex users or a JSON web token (JWT) for guest users without a Cisco Webex account.

---

This article provides code examples explaining how to perform this authorization using either a built in Webview or an external browser.

## Selected section

## Authorize Using an External Browser

As an alternative, `OAuthAuthenticator` can be used, which eliminates the need for a WebView. Developers have the flexibility to use any browser or WebView for authentication and then provide the authorization code to the SDK through `OAuthAuthenticator`:

```kotlin
val clientId: String = "YOUR_CLIENT_ID"
val clientSecret: String = "YOUR_CLIENT_SECRET"
val redirectUri: String = "https://webexdemoapp.com"
val scope: String = "spark:all"
val email = "EMAIL_ID_OF_END_USER" // Email address for the end user.

val authenticator: OAuthAuthenticator = OAuthAuthenticator(clientId, clientSecret, scope, redirectUri, email)
val webex = Webex(application, authenticator)

webex.initialize(CompletionHandler { result ->
    if (result.error == null) {
        // Already authorized
    } else {
        authenticator.getAuthorizationUrl(CompletionHandler { result ->
            if (result.error != null) {
                // Handle the error
            }else{
                // result.data
                // Use this URL to launch in either Webview or a web browser and then pass the authCode to the Authenticator's authorize method.
            }
        })
    }
})

authenticator.authorize(authCode, CompletionHandler { result ->
    if (result.error != null) {
        // Handle the error
    }else{
        // Authorization successful
    }
})
```
