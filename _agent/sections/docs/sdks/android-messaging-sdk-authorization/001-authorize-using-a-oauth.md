---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-authorization
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Authorize Using a OAuth
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-authorization). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-authorization.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication Event Delegate](005-authentication-event-delegate.md)

## Article introduction

The Webex Mobile Android SDK must be initialized and authorized to interact with the Webex platform. Your application should authenticate users through an [OAuth](https://oauth.net/) grant flow for existing Cisco Webex users or a JSON web token (JWT) for guest users without a Cisco Webex account.

---

This article provides code examples explaining how to perform this authorization using either a built in Webview or an external browser.

## Selected section

## Authorize Using a OAuth

`OAuthWebViewAuthenticator` utilizes a WebView for user authentication. Ensure the WebView is integrated into the view hierarchy before invoking the `authorize` method.

Initialize a `Webex` instance with [OAuth](https://oauth.net/) authentication:

```kotlin
val clientId: String = "YOUR_CLIENT_ID"
val clientSecret: String = "YOUR_CLIENT_SECRET"
val redirectUri: String = "https://webexdemoapp.com"
val scope: String = "spark:all"
val email = "EMAIL_ID_OF_END_USER" // Email address for the end user.

val authenticator: OAuthWebViewAuthenticator = OAuthWebViewAuthenticator(clientId, clientSecret, scope, redirectUri, email)
val webex = Webex(application, authenticator)

webex.initialize(CompletionHandler { result ->
    if (result.error == null) {
        // Already authorized
    } else {
        authenticator.authorize(loginWebview, CompletionHandler { result ->
                if (result.error != null) {
                    // Handle the error
                }else{
                    // Authorization Successful
                }
            })
    }
})
```
