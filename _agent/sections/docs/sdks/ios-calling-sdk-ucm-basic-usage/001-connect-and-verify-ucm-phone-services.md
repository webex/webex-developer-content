---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-ucm-basic-usage
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Connect and Verify UCM Phone Services
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-ucm-basic-usage). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-ucm-basic-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Follow the steps in this guide to begin using Cisco Unified Communications Manager (CUCM, or UCM for short) in your iOS application.

## Selected section

## Connect and Verify UCM Phone Services

Developers who want to utilize UCM features must first log in to UCM and ensure that phone services are connected.

To connect and verify the UCM phone services:

1. Start UC Services

    ```swift
    webex.startUCServices()
    ```

1. Check the UCM login status:

    ```swift
    var isUCLoggedIn = webex.isUCLoggedIn()
    if(isUCLoggedIn) {
        // Successfully logged into the CUCM service.
    }
    ```

1. Initiate the login to UCM by setting a domain or server URL:

   

> **Info**
>
> Provide either a domain or a server URL, but not both.



    ```swift
    webex.ucLoginDelegate = self // Always ensure ucLoginDelegate is set before invoking the method below.
    webex.setUCDomainServerUrl(ucDomain: "cucm.example.com", serverUrl: "cucmserver.example.com")
    ```

1. Implement the `WebexUCLoginDelegate` interface to handle asynchronous UCM callbacks:

    ```swift
    class YourViewController: UIViewController {
        override func viewDidAppear(_ animated: Bool) {
            // You need to register your class as a delegate.
            webex.ucLoginDelegate = self
        }
    }

    extension HomeViewController: WebexUCLoginDelegate {
        func onUCLoggedIn() {
            // CUCM login attempt was successful.
        }

        func onUCLoginFailed() {
            // CUCM login attempt failed.
        }
        
        func onUCServerConnectionStateChanged(status: UCLoginServerConnectionStatus, failureReason: PhoneServiceRegistrationFailureReason) {
            if status == .Connected {
                // CUCM server connection success.
            }
        }
        
        func loadUCSSOView(to url: String) {
            // If your CUCM server supports SSO-based sign-in, you'll need to open a webview using the webex.getUCSSOLoginView helper as shown below:
            webex.getUCSSOLoginView(parentViewController: self, ssoUrl: url) { success in
                if let success = success, success {
                    // You're logged in                
                }
            }
        }
        
       func onUCSSOLoginFailed(failureReason: UCSSOFailureReason) {
            // If the SSO login fails due to reasons such as session expiry, you'll need to re-login using the webex.retryUCSSOLogin helper as shown below: 
            webex.retryUCSSOLogin()
       }

        func showUCNonSSOLoginView() {
            // If your UCM server requires a non-SSO (username/password) flow, this delegate method will be invoked.
            // You should collect the username and password from the user and call the method below: 
            webex.setCUCMCredential(username: "user@example.com", password: "SuperSecret")
        }
    }
    ```

1. Check the server connection status:

    ```swift
    let status = webex.getUCServerConnectionStatus()
    if status == .Connected {
        // You're successfully connected to a UCM server.
    }
    ```

You can now start using UCM phone services.
