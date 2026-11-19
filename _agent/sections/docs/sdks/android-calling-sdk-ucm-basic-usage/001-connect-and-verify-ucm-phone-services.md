---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-ucm-basic-usage
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Connect and Verify UCM Phone Services
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-ucm-basic-usage). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-ucm-basic-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Follow the steps in this article to begin using Cisco Unified Communications Manager (CUCM, or UCM for short) in your Android application.

---

# Android Calling SDK | UCM Basic Usage

Follow the steps in this article to begin using Cisco Unified Communications Manager (CUCM, or UCM for short) in your Android application.

## Selected section

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
