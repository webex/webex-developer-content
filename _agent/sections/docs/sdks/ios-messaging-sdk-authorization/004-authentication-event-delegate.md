---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-authorization
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Authentication Event Delegate
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-messaging-sdk-authorization). [Full Markdown](../../../../../docs/sdks/ios-messaging-sdk-authorization.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [OAuth Authentication](001-oauth-authentication.md) [JWT Authentication](002-jwt-authentication.md) [Access Token Authentication](003-access-token-authentication.md)

## Article introduction

The Webex mobile SDK requires initialization and authorization to interact with the Webex platform. Your app must authenticate users either through an [OAuth](https://oauth.net/) grant flow for Cisco Webex users, or a [JSON Web Token (JWT)](https://developer.webex.com/docs/guest-issuer) for guest users without a Cisco Webex account.

---

This article discusses the methods for authorizing a `Webex` instance.

## Selected section

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
