---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Embedded App Configuration Options
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

## Embedded App Configuration Options

The following lists and describes the fields available when [creating or editing an embedded app](https://developer.webex.com/docs/embedded-apps-guide#creating-an-embedded-app-in-the-developer-portal) in the **Embedded App** submit form.

**Where does your app work?** &mdash; Specifies whether your app works inside of Webex Meetings, Messaging spaces (direct or group), in the Webex Sidebar or inside all 3 contexts.

**Embedded app name** &mdash; Name of the app as it appears in its App Hub listing, the Apps Gallery, and while running in the Webex app or Meeting Client.

**Description** &mdash; Long-form description (1024 characters maximum) of your application that should explain what your embedded app does, how it benefits users and, most importantly, how a user can get started using it. The field supports Markdown-formatted links, and ordered unordered lists, as shown below.

```plaintext
    [Link text](http://www.example.com/)

    Features:
    * Unordered lists can use asterisks
    1. Numbered lists
```

**Summary** &mdash; A shorter version of your app's **Description** field that appears on the app's listing page in App Hub (256 character maximum).

![App Summary](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt68eb728670b48ed2/62684113f8819866142d8121/app-summary-example.png)

**Tagline** &mdash; Taglines give Webex users a very short and catchy idea of what your app is about and appears below your app’s name in the Apps Gallery (24 character maximum).

![Tagline in Apps Gallery](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt30df407e4e0809fe/62684074e6785a6b4b46bebf/tagline-app-card-1.png)



> **Info**
>
> The **Tagline** field does not appear when creating your app, only when editing an existing app.



**Icon** &mdash; Icon displayed in the app's App Hub listing, the Apps Gallery, and the app's title bar.

**Valid domains** &mdash; List of valid domains you will use as the start URL(s) for your embedded app, or as URLs shared with others by call to [setShareUrl()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+setShareUrl).

**Start Page URL** &mdash; The URL that opens when a user opens your app from the Apps Gallery. This URL must be available over a secure (HTTPS) connection. You can also override this URL with specific URLs per context (see below).

The following options are available to meeting-based apps:

**In-meeting start page URL** &mdash; You can optionally override the URL specified by **Start Page URL** with a unique start page URL for meeting-based apps. If not specified then **Start Page URL** will be used.

**Layout preference** &mdash; Lets you specify if content you share with meeting participants via **Open for all** opens in the side panel (the default) or in the main meeting view.

![Layout preference](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1abb50b400c3d390/62a903bfa9454a5197099641/layout_preference.png)

The following options are available to messaging-based apps:

 **Space start page URL** &mdash; You can optionally override the URL specified by **Start Page URL** with a unique start page URL for messaging-based apps. If not specified then **Start Page URL** will be used.
 
The following options are available to Sidebar-based apps:

**Sidebar start page URL** &mdash; You can optionally override the URL specified by **Start Page URL** with a unique start page URL for Sidebar-based apps. If not specified then **Start Page URL** will be used.

**Sidebar behavior** &mdash; Check-box to indicate if the app can be configured to be always ON or not. Always ON apps are launched when the Webex app is launched and are beneficial for use cases where the app need to listen to events all the time. May also require enabling PII (Personally Identifiable Information) in case events have personal information.
