---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-api-reference
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Framework Versioning and API Support
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-api-reference). [Full Markdown](../../../../docs/embedded-apps-api-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This is the complete API reference for the Webex Embedded Apps 1.x Framework.

---



> **Warning**
>
> The Embedded Apps version 1 SDK has been deprecated and will be supported based upon the following [support policy](https://developer.webex.com/docs/webex-api-and-sdk-support-policy#current-end-of-life-eol-notices). For new customers accessing this page, please see the [Embedded Apps version 2 SDK API Reference](https://eaf-sdk.webex.com/). For existing version 1 SDK customers, please see [Migration from 1.x to 2.x](https://eaf-sdk.webex.com/#migration-from-1x-to-2x). New features will only be added to the version 2 SDK.

## Selected section

## Framework Versioning and API Support

The latest version of the Embedded Apps Framework is **1.5.0**. Different client apps (Webex app or Meeting Center, for example) may support different versions of the framework. Each API entry in this reference has an **Available Since** field that specifies the minimum SDK version required to use that API. Your app can use the [app.isSdkSupported()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+isSdkSupported) to determine if the client supports that version.

For example, the reference entry for [initiateSystemBrowserOAuth()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+initiateSystemBrowserOAuth) indicates that it's been available since version 1.5.0 of the SDK. The following code first checks if the client supports that SDK version before calling the method.

  ```javascript
  if(app.isSdkSupported("1.5.0")) {
      app.initiateSystemBrowserOAuth("https://signin.example.com/...")
          .then(function (response) { ... })
          .catch(function (error) { ... })
  }
  ```

Notes:

* The framework supports `major.minor` and `major.minor.patch` versioning. For example, "1.4" and "1.4.1" are valid version string formats, but "1" or "1.4.5.1" are not. 
* Version "1.4" is identical to "1.4.0".
