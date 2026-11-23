---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-basic-webex-calling-usage
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Register for Callbacks
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-basic-webex-calling-usage). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-basic-webex-calling-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the fundamental steps for integrating call functionality using the Webex iOS SDK.

## Selected section

## Register for Callbacks

To initiate and receive calls, the phone services must be operational. After signing into Webex, authentication for Webex calling phone services occurs automatically via Single Sign-On (SSO). An application can register the `WebexUCLoginDelegate` to determine when the phone services are ready. The `onUCServerConnectionStateChanged` callback indicates the connection status of the phone services, showing `UCLoginServerConnectionStatus.Connected` when available for use:

```swift
class YourViewController: UIViewController {
    override func viewDidAppear(_ animated: Bool) {
        // You need to register your class as a delegate.
        webex.ucLoginDelegate = self
    }
}

extension HomeViewController: WebexUCLoginDelegate {
    func onUCLoggedIn() {
        // Login is successful.
    }
    
    func onUCLoginFailed() {
        // Login attempt failed.
    }
    
    func onUCServerConnectionStateChanged(status: UCLoginServerConnectionStatus, failureReason: PhoneServiceRegistrationFailureReason) {
        if status == .Connected {
            // Server connection success.
        }
    }
    
    func showUCSSOLoginView(to url: String) {
        webex.getUCSSOLoginView(parentViewController: self, ssoUrl: url) { success in
            if let success = success, success {
                // You're logged in.
            }
        }
    }
    
    func showUCNonSSOLoginView() {
        webex.setCallServiceCredential(username: "user@example.com", password: "SuperSecret")
    }
}
```
