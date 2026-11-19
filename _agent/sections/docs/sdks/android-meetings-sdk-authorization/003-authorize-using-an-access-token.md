---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-authorization
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Authorize Using an Access Token
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-authorization). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-authorization.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication Event Delegate](005-authentication-event-delegate.md)

## Article introduction

The Webex Mobile Android SDK must be initialized and authorized to interact with the Webex platform. Your application should authenticate users through an [OAuth](https://oauth.net/) grant flow for existing Cisco Webex users or a JSON web token (JWT) for guest users without a Cisco Webex account.

---

This article provides code examples explaining how to perform this authorization using either a built in Webview or an external browser.

## Selected section

## Authorize Using an Access Token
`TokenAuthenticator` utilizes a access token for user authentication. Create a new `Webex` instance using access token authentication



> **Info**
>
> For guest users created using the new Service Apps based [Guest Management](https://developer.webex.com/create/docs/sa-guest-management), the generated guest's token should be used with Access Token-based authentication flow.



```kotlin
val token: String = "<your-access-token>"
 val expiryInSeconds = 60      // Expiry time in seconds
 val authenticator: TokenAuthenticator = TokenAuthenticator()
 val webex = Webex(application, authenticator)
 webex.initialize(CompletionHandler { result ->
     if (result.error == null) {
         // Already authorised
     } else {
         authenticator.authorize(token, expiryInSeconds, CompletionHandler { result ->
                 if (result.error != null) {
                     // Handle the error
                 }else{
                     // Authorization successful
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
