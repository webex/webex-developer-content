---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Creating an Embedded App in the Developer Portal
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

## Creating an Embedded App in the Developer Portal

You use the [New Embedded App](https://developer.webex.com/my-apps/new/embedded-app) form to create an embedded app. See [Embedded App Configuration Options](https://developer.webex.com/docs/embedded-apps-guide#embedded-app-configuration-options) for description of form fields.

**To create an embedded application:**

1. [Login](https://developer.webex.com/login) to the Developer Portal and open the [New Embedded App](https://developer.webex.com/my-apps/new/embedded-app) submission page.

    ![Developer Portal](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt84d239b19f5c1ec2/642dce1fcc01de1087084370/dev_portal.png)

2. Select or enter values for the embedded app's [configuration options](https://developer.webex.com/docs/embedded-apps-guide#embedded-app-configuration-options).

3. Click **Add Embedded App**.

    ![App submission confirmation](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf520e9c0904c5e37/642dce1f6c90a41201400690/success_adding_app.png)

At this point your application is in development mode and is available for your personal use in Webex meetings, messaging spaces or Sidebar. You can [request approval](https://developer.webex.com/docs/embedded-apps-guide#request-approval) of the application so others in your organization can also use it.
