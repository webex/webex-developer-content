---
type: Guide
title: Android Messaging SDK | Authorization
display_title: Authorization
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-authorization
content_type: documentation
product_group:
- webex-suite
categories:
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-messaging-sdk-authorization)

The Webex Mobile Android SDK must be initialized and authorized to interact with the Webex platform. Your application should authenticate users through an [OAuth](https://oauth.net/) grant flow for existing Cisco Webex users or a JSON web token (JWT) for guest users without a Cisco Webex account.

---

This article provides code examples explaining how to perform this authorization using either a built in Webview or an external browser.

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

## Authentication Event Delegate

Extend the `WebexAuthDelegate` interface to receive authentication-related event callbacks.

```kotlin
interface WebexAuthDelegate {
    /**
     * This notifies when user is logged out and re-login is required.
     */
    fun onReLoginRequired() {}
}
```

Example usage:

```kotlin
class SomeClass : WebexAuthDelegate {
    ...
    override fun onReLoginRequired() {
        // Handle signout and perform any cleanup if required.
    }
    ...
}
```
