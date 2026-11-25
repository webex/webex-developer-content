---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Managing Private Embedded Apps
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

## Managing Private Embedded Apps



> **Info**
>
> Private embedded apps are the only publishing option available for Webex for Government (FedRAMP).



Members of a Webex organization can [create a new Embedded App](https://developer.webex.com/docs/embedded-apps-guide#creating-an-embedded-app-in-the-developer-portal) in the Developer Portal. By default, such apps are considered _in-development_ and are only available to the user who created the app. They are not visible to any other Webex users in the same organization. A _private_ app is an in-development app that has been approved by an org administrator for use by some or all of its members. Note the following about private apps:

* They are not available on [App Hub](https://apphub.webex.com) or to users outside your organization.
* They don't need to be submitted to Cisco for any kind of approval. Webex organization admins have full control what apps are available to their users.
* Apps can be made available to all or some of the users in a Webex organization.

One use case for a private app is an existing internal app &mdash; a note taking app, for example &mdash; that a Webex org wants to make available to all of its users. Another example is an app under development to be submitted to App Hub that first needs internal beta testing. The org admin can make the app available to a select group of users for testing purposes.

Admins use [Control Hub](https://admin.webex.com) to approve in-development apps for use within their Webex organization(s).

**To approve a private app for use within an Webex organization**:

1. Sign in to [Control Hub](https://admin.webex.com) as a full administrator, and click the [Embedded Apps](https://admin.webex.com/apps/embeddedApps) tab.
2. Click the **Private** tab to view a list of currently approved private apps and in-development apps for which approval [has been requested](https://developer.webex.com/docs/embedded-apps-guide#request_approval) by the app developer.

    ![Control Hub](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb821d233ab638c09/62d9c07a57ac0577de0b9022/control-hub-apps.png)

    To include apps in the list that are in-development but have not yet requested approval, click the **Show In-Development Apps** option.

    ![Option to list in-development apps](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1b4e39bc9daf1f4d/62d9bfc0d2f5267009abe84b/list-in-dev-apps.png)

3. Select the private app you want to approve.
4. Select **Approved** under **Submission Status** and then do one of the following:

   * Select **All Users** to make the app available to all users in the organization.
   * To make the app available to a subset of users, click **Select Groups** and then select the group or groups you want to have access. See [About Per-Group and Per-User Access](https://developer.webex.com/docs/embedded-apps-guide#about-pergroup-and-peruser-access) for information about creating groups.

    ![App approval](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt57cc8826bfd72cbb/62d9c6d75c954177895a971d/approving-app.png)

5. Click **Done**. The app will now be available in the Apps Gallery in a Webex meeting or space.

<a id="request-approval"></a>

### Requesting Approval of an Embedded Apps for Internal Use

When a Webex user creates a new embedded app in the Developer Portal the app is considered to be _in-development_. In-development apps are only available in the Webex app to the user who created the app in the Developer Portal. The developer of an embedded app can request approval from the admin to make it available to other users in the developer's Webex organization.

**To request approval of your app for internal use**:

1. Open your [My Apps](https://developer.webex.com/my-apps) page in the Developer Portal.
2. Click the app you want to have approved.
3. On the app details page click **Request admin approval**.

  ![Request admin approval button](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta012892cea03ad06/6115dc5921157414bc0e1551/admin_approval.png)

The current submission status is displayed.
