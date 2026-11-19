---
type: Guide
title: Enabling Developer Tools TEST
display_title: Enabling Developer Tools TEST
canonical_url: https://developer.webex.com/docs/ea-developer-tools-test
content_type: documentation
product_group:
- webex-suite
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/ea-developer-tools-test)

---

**[Embedded Apps Guide](https://developer.webex.com/docs/ea-developer-guide-test) > Enabling Developer Tools**
* * * 

## Enabling Developer Tools in Meeting Client and Webex

To test and debug your embedded app while it runs in the Webex or Meeting Center client, you can use the standard developer tools available in Chrome and other modern web browsers. You first need to set a system flag or preference on your development system to enable access to developer tools.



> **Info**
>
> Developer tools are currently unavailable to messaging-based apps running in the Webex client on Windows systems. They are available to meeting-based apps running in Meeting Center on Windows.



**To enable developer tools in the Meeting Center client on Windows and MacOS**:

* On **Windows**, set `EnableEmbeddedAppDebug` to `1` in the `Computer\HKEY_CURRENT_USER\SOFTWARE\WebEx\DeveloperTools` registry key.

    ![Windows Registry key/value to enable debugging](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf71da76e63e39ab8/6137f7094a026a122d2b6c5d/enable_dev_tools_windows.png)

* On **MacOS**, run the following command:

    ```shell
    defaults write NSGlobalDomain WebexWebAppDeveloperExtras -bool true
    ```

**To enable developer tools in the Webex client on MacOS**:

* On **MacOS**, create an empty file named `cisco_spark_enable_webinspector.txt` and save it to your Mac's Desktop folder, for example:

    ```shell
    touch ~/Desktop/cisco_spark_enable_webinspector.txt
    ```

To open the developer tools, right-click (or Ctrl-click) anywhere inside the app's viewport and select **Inspect Element**. A **Reload** button also appears in the context menu, which you use to reload changes to your embedded app's assets.

![Web inspector for embedded app](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt65112bf7825e3644/61776cd8ac68a827432693b2/inspect_element.png)
