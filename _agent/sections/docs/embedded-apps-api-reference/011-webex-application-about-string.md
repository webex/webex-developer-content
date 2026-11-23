---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-api-reference
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Classes
- 'webex.Application.about : string'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-api-reference). [Full Markdown](../../../../docs/embedded-apps-api-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This is the complete API reference for the Webex Embedded Apps 1.x Framework.

---



> **Warning**
>
> The Embedded Apps version 1 SDK has been deprecated and will be supported based upon the following [support policy](https://developer.webex.com/docs/webex-api-and-sdk-support-policy#current-end-of-life-eol-notices). For new customers accessing this page, please see the [Embedded Apps version 2 SDK API Reference](https://eaf-sdk.webex.com/). For existing version 1 SDK customers, please see [Migration from 1.x to 2.x](https://eaf-sdk.webex.com/#migration-from-1x-to-2x). New features will only be added to the version 2 SDK.

## Parent context

## Classes

Classes defined by the framework.

* [Webex.Application](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application) &mdash; Main Webex application object.
  * [webex.Application.deviceType](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+deviceType) : string
&mdash; Form factor of client device.
  * [webex.Application.isPrivateDataAvailable](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+isPrivateDataAvailable) : boolean
&mdash; Indicates if the SDK returns real or derived values for PII.
  * [webex.Application.displayContext](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+displayContext) : string
&mdash; App&#x27;s display context.
  * [webex.Application.isShared](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+isShared) : boolean
&mdash; Indicates if a URL has been shared with a meeting or space.
  * [webex.Application.embeddedSdkVersion](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+embeddedSdkVersion) : string
&mdash; Version of the SDK embedded in the Webex or Meeting Center client.
  * [webex.Application.sdkVersion](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+sdkVersion) : string
&mdash; Minimum SDK version supported by the Webex or Meeting Center client.
  * [webex.Application.theme](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+theme) : string
&mdash; Color theme selected by the user for Webex or Meeting Center app.
  * [webex.Application.about](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+about) : string
&mdash; General information about the client application.
  * [webex.Application.language](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+language) : string
&mdash; Language code of the language being used by the client.
  * [webex.Application.setShareUrl(internalUrl, externalUrl, title, optionals)](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+setShareUrl) ⇒ Promise.&lt;number&gt;
&mdash; Specifies URL to share in a meeting or space.
  * [webex.Application.clearShareUrl()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+clearShareUrl)
&mdash; Clears the URL previously set with &#x60;setShareUrl()&#x60;.
  * [webex.Application.initiateSystemBrowserOAuth(authenticateUrl)](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+initiateSystemBrowserOAuth) ⇒ Promise.&lt;string&gt; \| number
&mdash; Initiates a single sign-On authentication flow with a third-party identity provider in the system web browser at the specified URL.
  * [webex.Application.on(eventName, callback)](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+on)
&mdash; Called when the specified [event](https://developer.webex.com/docs/embedded-apps-api-reference#events) is raised.
  * [webex.Application.off(eventName)](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+off)
&mdash; Stops listening for the specified [event](https://developer.webex.com/docs/embedded-apps-api-reference#events).
  * [webex.Application.listen()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+listen) ⇒ Promise.&lt;void&gt;
&mdash; Registers application to listen for specified events..
  * [webex.Application.stopListening()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+stopListening)
&mdash; Stops listening to all events.
  * [webex.Application.onReady()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+onReady) ⇒ Promise.&lt;void&gt;
&mdash; Called when the &#x60;Webex.Application&#x60; object has been initialized and the SDK is ready for use by your app.
  * [webex.Application.openUrlInSystemBrowser(url)](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+openUrlInSystemBrowser) ⇒ Promise.&lt;void&gt;
&mdash; Opens a URL in the default system browser.
  * [webex.Application.isSdkSupported(version)](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+isSdkSupported) ⇒ boolean
&mdash; Helper function which indicates if current API version is supported by the given client
  * [Webex.Application.ErrorCodes](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application.ErrorCodes)
&mdash; Error codes returned by the API.
* [Webex.Application.Context](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application.Context) &mdash; Application context object.
  * [webex.Application.Context.getUser()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application.Context+getUser) ⇒ [Promise.&lt;User&gt;](https://developer.webex.com/docs/embedded-apps-api-reference#User) \| number
&mdash; Returns information about the current user.
  * [webex.Application.Context.getMeeting()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application.Context+getMeeting) ⇒ [Promise.&lt;Meeting&gt;](https://developer.webex.com/docs/embedded-apps-api-reference#Meeting) \| number
&mdash; Returns information about the meeting the app is running in.
  * [webex.Application.Context.getSpace()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application.Context+getSpace) ⇒ [Promise.&lt;Space&gt;](https://developer.webex.com/docs/embedded-apps-api-reference#Space) \| number
&mdash; Returns information about the space the app is running in.
* [Meeting](https://developer.webex.com/docs/embedded-apps-api-reference#Meeting) &mdash; 
  * [meeting.isPresenting](https://developer.webex.com/docs/embedded-apps-api-reference#Meeting+isPresenting) : boolean
&mdash; Indicates if a URL has been shared with a meeting. URL sharing is not supported for spaces.
  * [meeting.setPresentationUrl(url, title, shareOptimizationMode, includeAudio)](https://developer.webex.com/docs/embedded-apps-api-reference#Meeting+setPresentationUrl) ⇒ Promise.&lt;number&gt;
&mdash; Specifies URL to be presented in a meeting, for example, a PDF or PowerPoint document. The URL will be rendered in the stage view after consent from the host. The first time the call is made, the **Share this app content** button is displayed. Additional calls to the &#x60;setPresentation&#x60; URL will not require consent after the initial consent request from the host.
&#x60;setPresentationUrl&#x60; can be called multiple times but subsequent calls will return &#x60;INVALID_ARGUMENT&#x60; if the app developer changes either the &#x60;optimizationMode&#x60; or the &#x60;includeAudio&#x60; parameter while the share is ongoing. To change &#x60;optimizationMode&#x60; or &#x60;includeAudio&#x60; you must manually stop the share, update the parameters and restart the share.
  * [meeting.clearPresentationUrl()](https://developer.webex.com/docs/embedded-apps-api-reference#Meeting+clearPresentationUrl)
&mdash; Clears the URL previously set with &#x60;setPresentationUrl()&#x60;.

<a name="Webex.Application"></a>

## Selected section

### webex.Application.about : string

General information about the client application.

**Available since**: 1.1.0

Contains general information about the client app (Webex or Meeting Center) in which the app is running. This format is subject to change and should only be used for diagnostic purposes.

* * *

<a name="Webex.Application+language"></a>
