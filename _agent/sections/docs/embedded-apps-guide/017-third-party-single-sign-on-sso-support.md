---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Third-Party Single Sign-On (SSO) Support
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-guide). [Full Markdown](../../../../docs/embedded-apps-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

The general approach to developing embedded apps is similar to developing any other web app.

---

The main difference is that your app runs within the context of a Webex Meeting or Space, rather than in an external web browser. Embedded apps integrate with the Embedded App Framework to enable the following features:

* Ability to start an "Open for all" session with Meeting participants, or "Add to Tab" functionality in a Space.
* Get information about the meeting or messaging space host and user information (if permitted by the user or organization), Webex or Meeting Center theme color (light or dark, for example), and other details.
* Respond to events emitted by the framework about changes to the app's environment (theme change, for example), changes to the meeting host or space , or display context (sidebar or pop-out window).



> **Success**
>
> As of Webex app version 44.3, we’ve integrated the Webex AppHub natively into the Webex app itself, allowing your users to explore Apphub to discover apps and bots without the need to leave the Webex application! For more information, see [What's New](https://developer.webex.com/docs/embedded-apps-whats-new).





> **Info**
>
> If you are not currently a Webex customer you can [request a developer sandbox](https://developer.webex.com/docs/developer-sandbox-guide) to start developing embedded apps. Free Webex user accounts cannot be used to create embedded apps.





> **Info**
>
> The Embedded Apps version 1 SDK has been deprecated and will be supported based upon the following [support policy](https://developer.webex.com/docs/webex-api-and-sdk-support-policy#current-end-of-life-eol-notices). For new customers accessing this page, please see the [Embedded Apps version 2 SDK API Reference](https://eaf-sdk.webex.com/). For existing version 1 SDK customers, please see [Migration from 1.x to 2.x](https://eaf-sdk.webex.com/#migration-from-1x-to-2x). New features will only be added to the version 2 SDK.



The basic workflow for developing embedded apps is as follows:

1. Create an embedded app in the [Webex Developer Portal](), providing the HTTPS URL of your app's starting page. At this point your app is in development mode is only visible to your Webex account.
2. [Enable Developer Tools](https://developer.webex.com/docs/embedded-apps-guide#enabling-developer-tools) in Meeting Center or Spaces so you can debug your app within the embedded context.
3. Open the app in a Meeting or Space to test it. Publish changes or fixes to your web host, and use the **Reload** menu item available the right-click/control-click context menu to reload your app's resources. In this way you can quickly iterate on changes directly in the Meeting or Space.

## Selected section

## Third-Party Single Sign-On (SSO) Support



> **Warning**
>
> `initiateSystemBrowserOAuth` is not supported in Webex for Government (FedRAMP).



Embedded apps can use third-party SSO providers to authenticate their users using the [initiateSystemBrowserOAuth()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+initiateSystemBrowserOAuth) method. Since some identity providers have security policies that prevent the OAuth flow from completing in an embedded browser, `initiateSystemBrowserOAuth()` delegates the OAuth SSO authorization flow to the system browser.

Notes:

* The `initiateSystemBrowserOAuth()` method returns an authorization code after the user authenticates with the ID provider. The embedded app is responsible for exchanging the authorization token for an access token or ID token from the ID provider.
* The **redirect_uri** parameter of the authorization URL passed to `initiateSystemBrowserOAuth()` must be set to **https://oauth-helper-prod.wbx2.com/helperservice/v1/callback**. This URL points to a helper service managed by Webex that correlates the authorization code returned by the ID provider with the embedded app that made the request. 


> **Info**
>
> If you're developing an app for Webex for Government (FedRAMP), use the following callback URL: **https://oauth-helper.gov.ciscospark.com/helperservice/v1**.


* Your embedded app's **Valid domains** [configuration option](https://developer.webex.com/docs/embedded-apps-guide#embedded-app-configuration-options) must include the domain for the SSO page (**accounts.example.com**, for example).
* The Webex client appends a `state` parameter to the authorization URL set to a cryptographically random string. Apps should not add their own `state` parameter to the authorization URL as it will be over-written.
* The `initiateSystemBrowserOAuth()` method is supported by version 1.5 and later of the embedded apps SDK. You can use the [isSdkSupported](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+isSdkSupported) method to determine if this feature is available to your app. See [Framework Versioning and API Support](https://developer.webex.com/docs/embedded-apps-api-reference#framework-versioning-and-api-support) for more information.

The following code shows the basic code to initiate a single sign-on flow. The code to exchange the authorization code for an access or ID token is not shown.

```javascript
// Variable to hold authorization code from ID provider
let authCode;
// Initiate SSO flow in system browser
app.initiateSystemBrowserOAuth("https://accounts.example.com/auth?client_id=...&redirect_uri=https://oauth-helper-prod.wbx2.com/helperservice/v1/callback")
  .then(function (response) {
    // Promise fulfilled, get authorization code from JSON response
    authCode = response;
    console.log(`Got authorization code: ${authCode}`)
    // Exchange authorization code for a token with ID provider. 
    // This part of the OAuth flow is the responsibility of the embedded app, for example:
    // exchangeCodeForToken(authCode);
  })
  .catch(function (reason) {
    console.error("initiateSystemBrowserOAuth() failed with reason=",
                   window.Webex.Application.ErrorCodes[errorcode]
    );
  }
```
