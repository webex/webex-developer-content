---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-reference
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Framework Versioning and API Support
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-reference). [Full Markdown](../../../../docs/embedded-apps-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

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
