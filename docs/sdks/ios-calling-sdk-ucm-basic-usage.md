---
type: Guide
title: iOS Calling SDK | UCM Basic Usage
display_title: Basic Usage
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-ucm-basic-usage
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-calling-sdk-ucm-basic-usage)

Follow the steps in this guide to begin using Cisco Unified Communications Manager (CUCM, or UCM for short) in your iOS application.

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

## Use UCM Phone Services

To use UCM phone services once you've verified your connection:

1. Make a call.

    Use `dialPhoneNumber` for PSTN or `dial` for other call types:

    ```swift
    let mediaOption = MediaOption.audioOnly()
     webex.phone.dialPhoneNumber("+1800123456", option: mediaOption) { result in
        switch result {
           case .success(let call):
                 // Call started successfully.
            case .failure(let error):
                // Call failed.
        }
    }
    ```

    

> **Info**
>
> The `dialPhoneNumber` API is available starting with version 3.9.2.



1. Transfer a call:

    ```swift
    guard call.isCUCMCall else { 
        print("Call transfer works only with UCM calls")
        return
    }

    // Put an active call on hold
    call.holdCall(putOnHold: true) { error in 
        if(error != nil) {
            // hold success
        }
    }
    
    // Start a new call that can be transferred later to the previous call
    call.startAssociatedCall( dialNumber: "+1800123123", associationType: .transfer, isAudioCall: true) {[weak self] result in
        switch result {
        case .success(let newCall):
            // Successfully started an associated call that can be transferred
            call.transferCall(toCallId: newCall.callId)
        case .failure(let error):
            // An error occurred
        }
    }  
    ```

1. Merge a call:

    ```swift
    guard call.isCUCMCall else { 
        print("Call merge works only with CUCM calls.")
        return
    }

    // Put an active call on hold:
    call.holdCall(putOnHold: true) { error in 
        if(error != nil) {
            // hold success
        }
    }
    
    // Start a new call that can be merged later with the existing call.
    call.startAssociatedCall(dialNumber: "+1800123123", associationType: .merge, isAudioCall: true) {[weak self] result in
        switch result {
        case .success(let newCall):
            // Merge the calls.
            call.mergeCall(targetCallId: newCall.callId)
        case .failure(let error):
            // An error occurred.
        }
    }  
    ```

## Flow Chart for UCM Logins

![UCM login flow chart.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltfe1de2625ef8f3aa/CUCM-flow-iOS-SDK.png)

## UCM Call Notifications

For information on handling UCM incoming call notifications, see: [App Registration For Mobile SDK v3](https://github.com/webex/webex-ios-sdk/wiki/App-Registration-for-Mobile-SDK-3.x).
