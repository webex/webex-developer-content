---
type: Guide
title: Android Calling SDK | UCM Basic Usage
display_title: Basic Usage
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-ucm-basic-usage
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-calling-sdk-ucm-basic-usage)

Follow the steps in this article to begin using Cisco Unified Communications Manager (CUCM, or UCM for short) in your Android application.

---

# Android Calling SDK | UCM Basic Usage

Follow the steps in this article to begin using Cisco Unified Communications Manager (CUCM, or UCM for short) in your Android application.

## Connect and Verify UCM Phone Services

Developers who want to utilize UCM features must first log in to UCM and ensure that phone services are connected.

To connect and verify the UCM phone services:

1. Start the UCM services:

    ```kotlin
    webex.startUCServices()
    ```

1. Check the UCM login status:

    ```kotlin
    val isUCLoggedIn = webex.isUCLoggedIn()
    if (isUCLoggedIn) {
        // Already logged in to the UCM service.
    } else {
        // Not logged into UCM service
    }
    ```

1. Initiate the login to UCM by setting a domain or server URL:

   

> **Info**
>
> Provide either a domain or a server URL, but not both.



    ```kotlin
    webex.setUCDomainServerUrl(ucDomain = "UCM.example.com", serverUrl = "")
    ```

1. Implement the `WebexUCLoginDelegate` interface to handle asynchronous UCM callbacks:

    ```kotlin
    class HomeActivity : WebexUCLoginDelegate {
        // Callbacks
        override fun onUCLoggedIn() {
            // UCM login attempt was successful.
        }

        override fun onUCLoginFailed() {
            // UCM login attempt failed.
        }

        override fun loadUCSSOViewInBackground(ssoUrl: String) {
            // If your UCM server supports SSO based sign in, you'll need to open a webview using `UCSSOWebViewAuthenticator.launchWebView` helper.
            UCSSOWebViewAuthenticator.launchWebView(webviewInstance, ssoUrl, CompletionHandler { result ->
                if (result.isSuccessful) {
                    // UCM login attempt was successful.
                } else {
                    // UCM login attempt failed.
                }
            })
        }

        override fun showUCNonSSOLoginView() {
            // This method is invoked if your UCM server requires a non-SSO (username/password) flow.
            // You should collect the username / password from the user and call the following method: 
            webex.setCUCMCredential(username = "user@example.com", password = "SuperSecret")
        }

        override fun onUCSSOLoginFailed(failureReason: UCSSOFailureReason) {
            // If the SSO login fails due to reasons such as session expiry, you'll need to re-login using the webex.retryUCSSOLogin helper as shown: 
            webex.retryUCSSOLogin()
        }

        override fun showUCSSOBrowser() {
            // Show the webview.
        }

        override fun hideUCSSOBrowser() {
            // Hide the webview.
        }

        override fun onUCServerConnectionStateChanged(status: UCLoginServerConnectionStatus, failureReason: PhoneServiceRegistrationFailureReason) {
            if (status == UCLoginServerConnectionStatus.Connected) {
                // UCM server connection success. Once connected you can start making and receiving calls.
            }
        }
    }
    ```

1. (**Optional**) If you encounter a `PhoneServiceRegistrationFailureReason.RegisteredElsewhere` failure, you can force registration on the current device:

    ```kotlin
    webex.forceRegisterPhoneServices()
    ```

1. Check the server connection status:

    ```kotlin
    val status = webex.getUCServerConnectionStatus()
    if (status == UCLoginServerConnectionStatus.Connected) {
        // You're successfully connected to a UCM server.
    }
    ```

You can now start using UCM phone services.

## Use UCM Phone Services

1. Make a call:

    Use `dialPhoneNumber` for PSTN or `dial` for other types.

    ```kotlin
    val mediaOption = MediaOption.audioOnly()
    webex.phone.dialPhoneNumber("+1800123456", mediaOption, CompletionHandler { result ->
        if (result.isSuccessful) {
            // Call started successfully, result.data gives you a Call object
        } else {
            // Call failed, result.error gives you the error code. The error code will be an instance of WebexError.ErrorCode
        }
    })
    ```

    

> **Info**
>
> The `dialPhoneNumber` API is available starting with version 3.9.2.



1. Transfer a call:

    ```kotlin
    // Hold the current ongoing call before associating to another call
    call?.holdCall(true, CompletionHandler { result ->
        if (result.isSuccessful) {
            // Call hold successful
        } else {
            // Call hold failed
        }
    })
    ```

    ```kotlin
    // Proceed if hold succeeds
    call?.startAssociatedCall("+1800123457", associationType = CallAssociationType.Transfer, audioCall = true, CompletionHandler { result ->
            if (result.isSuccessful) {
                // Call association is successful; result.data returns a new Call object.
                val newCall: Call? = result.data
                // Transfer the call.
                call?.transferCall(newCall?.getCallId())
            } else {
                // Call association failed.
            }
        })
    ```  

1. Merge a call:

    ```kotlin
    // Put the active call on hold.
    call?.holdCall(true, CompletionHandler { result ->
        if (result.isSuccessful) {
            // Call hold successful
        } else {
            // Call hold failed
        }
    })
    ```

    ```kotlin
    // If hold succeeds, start a new call that can be merged later with the existing call.
    call?.startAssociatedCall("+1800123457", associationType = CallAssociationType.Merge, audioCall = true, CompletionHandler { result ->
        if (result.isSuccessful) {
            // Call association is successful; result.data returns a new Call object.
            val newCall: Call? = result.data
            // Merge the calls.
            call?.mergeCalls(newCall?.getCallId())
        } else {
            // Call association failed.
        }
    })
    ```

1. Logout of UCM:

    ```kotlin
    webex.authenticator?.deauthorize(CompletionHandler { result ->
        if (result.isSuccessful) {
            // Logged out of UCM and Webex services successfully
        } else {
            // Logout failed; result.error?.errorMessage provides more details.
        }
    })
    ```

    

> **Info**
>
> If the SSO login is in progress and the user cancels the login flow, the SSO flow should be canceled by calling the `webex.ucCancelSSOLogin()` method.



## UCM Login Flow Chart

![UCM login flow chart](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2caac5a9ec0527f9/uc_login_flow.png)
