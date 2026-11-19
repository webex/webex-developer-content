---
type: Excerpt
canonical_url: https://developer.webex.com/docs/frequently-asked-questions
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Embedded Apps
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/frequently-asked-questions). [Full Markdown](../../../../docs/frequently-asked-questions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

If you don't find the answer you're looking for here, please contact Webex Developer Support.

## Selected section

## Embedded Apps

### I am new to Webex and want to develop an embedded app. How do I get started?

First you'll need to request a [Developer Sandbox](https://developer.webex.com/docs/developer-sandbox-guide) that will provide you with a test organization you can use to create embedded apps in the [Developer Portal](https://developer.webex.com/). Next, follow the [developer quick start](https://developer.webex.com/docs/embedded-apps-guide#developer-quick-start) to create, configure, and test your first embedded app, and get familiar with the Embedded Apps JavaScript Framework.

### My company is a Webex partner or customer. How do I get started developing an embedded app?

As a Webex partner or customer you can start creating embedded apps for your organization right away. Follow the [developer quick start](https://developer.webex.com/docs/embedded-apps-guide#developer-quick-start) to create, configure, and test your first embedded app. Also get familiar with the [Embedded Apps JavaScript Framework](https://developer.webex.com/docs/embedded-apps-api-reference).

If you'd prefer to try creating embedded apps outside of your main Webex organization, you can request a [Developer Sandbox](https://developer.webex.com/docs/developer-sandbox-guide.), which will provide you with a "dummy" organization for testing purposes.

### Do I need a Webex account to build an embedded app?

To create an embedded app you'll need to [request a Developer Sandbox](https://developer.webex.com/docs/developer-sandbox-guide), which will provide you with a test organization and a Webex admin account you can use to create and test embedded apps.

### Can I develop an application to be used only within my own Organization?

Yes, you can create a private app that--once approved by your Webex organization's administrator--can only be used by members of your organization. To request approval of a private embedded app click **Request Admin Approval** on your embedded app's configuration page in the [Developer Portal](https://developer.webex.com/my-apps/).

![Graphical user interface, text Description automatically generated](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf13fbb645b327b13/6227b5e9b130ac22c454cedf/devhub-submit.png)

### I'm an admin for a Webex organization. How do I approve private apps for use within my organization?

Webex organization admins can approve in-development apps from the Control Hub's [Embedded Apps view](https://admin.webex.com/apps/embeddedApps).

![Approve embedded application](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbdbd5e86375539aa/6227b5e82f117523f14add80/approve.png)

The following questions are related to access to personal information about embedded app users, as well as about the meeting or messaging space in which the app is running using the [Embedded Apps JavaScript API](https://developer.webex.com/docs/embedded-apps-api-reference).

### How can I get information about meeting participants or space members?

Currently, the embedded apps API doesn't provide a way to list or get information about meeting participants or messaging space members. It is possible to create a combined a Embedded App and Webex Integration solution that would let your application retrieve user information via the Webex REST APIs.

### Can my application access a user's Personally Identifying Information (PII), such as email or username?

By default, embedded apps do not have access to personally identifying information (PII) returned by the [getUser(),](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application.Context+getUser) [getMeeting(),](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application.Context+getMeeting) or [getSpace()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application.Context+getSpace) API methods. This setting can be controlled by the user's Webex organization administrator on a per-app basis.

By default, values that would contain PII are either blank (an empty string) or contain "derived" values. Derived values are opaque to third parties but are guaranteed to be consistent for a given user. This provides apps a way to associate a user with an application session even if access to PII is not permitted. For more information, see [Personally Identifiable Information (PII) and Embedded Apps](https://developer.webex.com/embedded-apps-guide#personally-identifiable-information-pii-and-embedded-apps).

### I am unable to get the meeting host's e-mail address via the embedded apps API. What am I missing?

Information about the meeting host is not currently available via the SDK, regardless of the app's setting for access to personal information The only user information provided by the SDK is for the meeting participants using the embedded app. For more information, see [Personally Identifiable Information (PII) and Embedded Apps](https://developer.webex.com/docs/embedded-apps-guide#personally-identifiable-information-pii-and-embedded-apps).

You can create a combined embedded app and [Webex integration](https://developer.webex.com/docs/integrations) solution to obtain information about the meeting host.

### Can I call Webex APIs directly from an embedded app?

Embedded apps cannot make direct calls to the [Webex APIs](https://developer.webex.com/docs/getting-started). However, you can create a combined solution consisting of an Embedded App and an [Integration](https://developer.webex.com/docs/integrations) to enable this type of application. In this scenario, your embedded app is assisted by a back-end process (the Integration) that makes Webex API calls on behalf of the embedded app. The embedded app displays the results of API calls handled by the Integration. For more information, see [About Combined Embedded App and Integration](https://developer.webex.com/docs/embedded-apps-guide#integrations) Solutions in the Embedded Apps Developer Guide.

### I'm an admin for my Webex organization. How can I enable access to personally identifiable information (PII) for a given app?

Webex organization admins can allow an app access to PII from the app's configuration page in Embedded Apps view on Control Hub.

![Personally Identifiable Information](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte2f4172e541f0d3e/6227b5e8737c7822c288104f/pii-dialog.png)

### What browser engines does Webex use to render embedded apps?

On MacOS, the platform's installed WebKit engine is used to render embedded apps running in both meetings and messaging spaces.

On Windows, Webex uses WebView2 for in-meeting apps, which is based on the same Chromium core as the Microsoft Edge browser; for apps running in messaging spaces, Webex currently uses the Chromium Embedded Framework (CEF).

On Linux, CEF is used for apps running in both meetings and messaging spaces.

### Do embedded apps have access to the user's microphone or camera?

For the initial phase of embedded apps, access to the user's camera and microphone/audio access is not supported.

### Can I use cookies or local storage in embedded apps?

Yes, cookies and local storage data that your application sets will be available if the user closes the Webex or Meeting Center client and opens it again later. For more information, see [Using Cookies and Local Storage](https://developer.webex.com/docs/embedded-apps-guide#cookies_local_storage).
