---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-basic-webex-calling-usage
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Register for Callbacks
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-basic-webex-calling-usage). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-basic-webex-calling-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the fundamental steps for integrating call functionality using the Webex Android SDK.

## Selected section

## Register for Callbacks

To initiate and receive calls, the phone services must be operational. After a user signs into Webex, authentication for Webex calling phone services occurs automatically via Single Sign-On (SSO). An application can register the `WebexUCLoginDelegate` to determine when the phone services are ready. The `onUCServerConnectionStateChanged` callback provides the phone services connection status, indicating `UCLoginServerConnectionStatus.Connected` when it is available for use:

```kotlin
private class UCDelegate() : WebexUCLoginDelegate{
    // Triggered when the application needs to hide the WebView that was loaded in `loadSSOViewInBackground`.
    override fun hideUCSSOBrowser() {
        super.hideUCSSOBrowser()
    }

    // Triggered when SSO authentication for the CUCM domain/server is required.
    // The given ssoUrl needs to be loaded in a WebView to start the authentication process.
    // This callback applies only to [com.ciscowebex.androidsdk.phone.Phone.CallingType.CUCM].
    override fun loadUCSSOViewInBackground(ssoUrl: String) {
        super.loadUCSSOViewInBackground(ssoUrl)
    }

    // Notify when the user is successfully logged in to the Webex Calling service.
    override fun onUCLoggedIn() {
        super.onUCLoggedIn()
    }

    // Notify the app whenever the server URL/domain, username, and password are required for authentication.
    // Application needs to display the option for entering required details.
    override fun onUCLoginFailed() {
        super.onUCLoginFailed()
    }

    // Triggered when an SSO login fails.
    override fun onUCSSOLoginFailed(failureReason: UCSSOFailureReason) {
        super.onUCSSOLoginFailed(failureReason)
    }

    // Triggered when the calling service connection status changes.
    override fun onUCServerConnectionStateChanged(status: UCLoginServerConnectionStatus, failureReason: PhoneServiceRegistrationFailureReason) {
        super.onUCServerConnectionStateChanged(status, failureReason)
        
        // UCLoginServerConnectionStatus indicates the phone services connection status.
    }

    // Triggered when the server URL/domain, username and password are required for authentication.
    // Application needs to display the option for entering required details.
    override fun showUCNonSSOLoginView() {
        super.showUCNonSSOLoginView()
    }

    // Triggered when the application needs to show the webview loaded in [loadSSOViewInBackground].
    override fun showUCSSOBrowser() {
        super.showUCSSOBrowser()
    }
}

//Save the delegate object into webex instance to register the callbacks.
...
webex?.delegate = UCDelegate()
...
```
