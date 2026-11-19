---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-authorization
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- OAuth Authentication
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-authorization). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-authorization.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [JWT Authentication](002-jwt-authentication.md) [Access Token Authentication](003-access-token-authentication.md) [Authentication Event Delegate](004-authentication-event-delegate.md)

## Article introduction

The Webex mobile SDK requires initialization and authorization to interact with the Webex platform. Your app must authenticate users either through an [OAuth](https://oauth.net/) grant flow for Cisco Webex users, or a [JSON Web Token (JWT)](https://developer.webex.com/docs/guest-issuer) for guest users without a Cisco Webex account.

---

This article discusses the methods for authorizing a `Webex` instance.

## Selected section

## OAuth Authentication

Use Webex OAuth authentication to authorize the `Webex` instance:

```swift
let clientId = "$YOUR_CLIENT_ID"
let clientSecret = "$YOUR_CLIENT_SECRET"
let scope = "spark:all" // Space separated list of scopes. spark:all is always required
let redirectUri = "https://webexdemoapp.com/redirect"

let authenticator = OAuthAuthenticator(clientId: clientId, clientSecret: clientSecret, scope: scope, redirectUri: redirectUri, emailId: "user@example.com")
let webex = Webex(authenticator: authenticator)
webex.enableConsoleLogger = true 
webex.logLevel = .verbose // It is highly recommended to make this end-user configurable in case detailed logs are needed.

webex.initialize { isLoggedIn in
        if isLoggedIn {
            print("User is authorized")
        } else {
            authenticator.authorize(parentViewController: self) { result in
            if result == .success {
                print("Login successful")
                webex.onInitialSpacesSyncCompleted = {
                    print("Spaces initial sync successful")
                }
            } else {
                print("Login failed")
            }
        }
    }
}
```

Alternatively, retrieve the authorization URL using `getAuthorizationUrl` method and pass the authorization code to the SDK using the `authorize` method:

```swift
webex.initialize {  isLoggedIn in
    if isLoggedIn {
        // Already authorised
    } else {
        authenticator.getAuthorizationUrl(completionHandler: { result, url in
            if result == .success {
                print(url)
                // Use this URL to launch in your own browser or WebView, then pass the authCode to the authorize() method.
            }
        })
    }
} 

authenticator?.authorize(oauthCode: code, completionHandler: { res in
    if res == .success {
    // success
    } else {
    // failure
    }
})
```
