---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Enabling Developer Tools
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

## Enabling Developer Tools

To test and debug your embedded app while it runs in the Webex or Meeting Center client, you can use the standard developer tools available in Chrome and other modern web browsers. You first need to set a system flag or preference on your development system to enable developer tools.

**To enable developer tools in Webex for Windows**:

1. Open the Registry Editor application.
2. Add a new registry key named **Cisco Spark Native** to **Computer\HKEY_LOCAL_MACHINE\SOFTWARE**.

    ![Create Spark key](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt87738f742f1685ea/6262e30ce6785a6b4b46b5e7/create-spark-key.png)

3. Add a new DWORD (32-bit) value named **EnableEmbeddedAppDebug** to the **Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Cisco Spark Native** registry key, and set its value to **1**. To disable, set to **0**.

    ![Windows Registry key/value to enable debugging](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb9d34c0a94665d88/623dfb29ddd8655f56f60d88/enable_webex_dev_tools_windows.png)

**To enable developer tools in Webex for MacOS**:

* Create an empty file named `cisco_spark_enable_webinspector.txt` and save it to your Mac's Desktop folder, for example:

    ```shell
    touch ~/Desktop/cisco_spark_enable_webinspector.txt
    ```

**To enable developer tools in Meeting Center for Windows and MacOS**:

1. Create a file named `featureToggle.xml`.
2. Add the following text:

    ```xml
   <featureToggles>
     <feature name="EnableEmbeddedAppsDevMode" isEnabled="1"/>
   </featureToggles>
   ```
   To enable the dev tools, set `isEnabled` to `1`. To disable, set to `0`.
3. Copy the file to the following location:

   **Windows**: `%USERPROFILE%`

   **Mac**: `~/Library/Application Support/Webex Meetings/AppData/`
4. Restart Webex.
5. For either platform, to display the dev tools, right click in your embedded app and choose **Inspect** from the context menu.

### Opening Developer Tools

* **To open the developer tools in Webex or Meeting Center for MacOS**, right-click (or Ctrl-click) anywhere inside the app's viewport and select **Inspect Element**.

    ![Web inspector for embedded app](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte5639e1ae7ee8720/62420026be1258179f9b1fb3/inspect-element.png)

* **To open the developer tools in Webex or Meeting Center for Windows**, right-click (or Ctrl-click) anywhere inside the app's viewport and select **Inspect**.

    ![Devtools in Meeting Center](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt29c2fc680d8a4bbe/6241e8b0e35a2b61570d8447/inspect-windows.png)
