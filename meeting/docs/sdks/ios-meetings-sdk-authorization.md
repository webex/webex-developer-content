---
type: Guide
title: iOS Meetings SDK | Authorization
display_title: Authorization
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-authorization
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-meetings-sdk-authorization)

The Webex mobile SDK requires initialization and authorization to interact with the Webex platform. Your app must authenticate users either through an [OAuth](https://oauth.net/) grant flow for Cisco Webex users, or a [JSON Web Token (JWT)](https://developer.webex.com/docs/guest-issuer) for guest users without a Cisco Webex account.

---

This article discusses the methods for authorizing a `Webex` instance.

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

authenticator?.authorize\(oauthCode: code, completionHandler: { res in
    if res == .success {
    // success
    } else {
    // failure
    }
})
```

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

## Access Token Authentication

Authorize the `Webex` instance using an access token.



> **Info**
>
> For guest users created using the new Service Apps based [Guest Management](https://developer.webex.com/create/docs/sa-guest-management), the generated guest's token should be used with Access Token-based authentication flow.



```swift
let authenticator = TokenAuthenticator\(isFedRAMPEnvironment: isFedRAMP\)
webex = Webex\(authenticator: authenticator\)
    authenticator.authorizedWith\(accessToken: token, expiryInSeconds: nil, completionHandler: { res in
    if res == .success {
    // Success.
    } else {
    // Failure.
    }
})
```

## Authentication Event Delegate

Register for the `WebexAuthDelegate` to receive authentication-related event callbacks, such as when re-authentication is required:

```swift
public protocol WebexAuthDelegate: AnyObject {
    /// Notifies when the user is logged out and re-login is required.
    /// Available since v3.11.2.
    func onReLoginRequired()
}
```

Usage:

```swift
extension AppDelegate: WebexAuthDelegate {
    func onReLoginRequired() {
        print("onReLoginRequired called")
    }
}

webex.authDelegate = UIApplication.shared.delegate as! AppDelegate
```
