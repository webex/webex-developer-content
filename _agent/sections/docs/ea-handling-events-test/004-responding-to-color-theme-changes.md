---
type: Excerpt
canonical_url: https://developer.webex.com/docs/ea-handling-events-test
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Responding to Color Theme Changes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/ea-handling-events-test). [Full Markdown](../../../../docs/ea-handling-events-test.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

**[Embedded Apps Guide](https://developer.webex.com/docs/ea-developer-guide-test) > Event Handling**
* * * 

## Selected section

## Responding to Color Theme Changes
<a id="color-theme-change-events"></a>

In the screenshot of the Open Together session shown previously you'll notice that the host and participant had different themes applied to their Meeting Center client. The white background of the shared URL looks good for the host (whose meeting window is set to use the light theme) but not as good for the participant who has selected the dark theme. Ideally, the application theme matches client application's theme.

In this section you'll add code that updates basic CSS styles in the shared application to match the currently selected theme. There are two parts to this:

* Setting color styles to match the theme setting on initial launch. You can get the current theme setting from the [`app.theme`](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+theme) property.
* Responding to theme changes the user makes in Webex or Meeting client, which generates an [`application:themeChanged`](https://developer.webex.com/docs/embedded-apps-api-reference#events) event.

**To make the app's colors match the selected theme**:

1. Open **shared.js** from the embedded app you created in the quick start.

2. Append the following code to the `onReady().then()` handler:

    ```javascript
        // Register event handler for themeChanged event:
        app.on('application:themeChanged', (theme) => {
            updateColorTheme(theme);
            log("Updating theme to", theme)
        })
    })
    ```

    When the `application:themeChanged` event is emitted the listener function calls a custom function named `updateColorTheme()`, passing it the event object containing the newly selected theme.

3. Add the `updateColorTheme()` function to shared.js:

    ```javascript
    function updateColorTheme(theme) {
        switch (theme) {
            case "LIGHT":
                document.body.style["background"] = "#FFFFFF";
                document.body.style["color"] = "#000000";
                break;
            case "DARK":
                document.body.style["background"] = "#121212";
                document.body.style["color"] = "#F7F7F7";
                break;
            default:
                break;
        }
    }
    ```

4. Lastly, for the app's colors to match the theme when the application starts, add following code to the app's `onReady()` handler.

    ```javascript
    updateColorTheme(app.theme)
    ```

    Your app's `onReady()` handler should look like the following:

    ```javascript
    app.onReady().then(() => {
        log("Application ready. App", app);
        app.context.getUser().then((user)=> {
            log("User ID", user.id)
        }).catch((errorcode) => {
            log("Error", errorcode)
        })
        // Register event handler for themeChanged event:
        app.on('application:themeChanged', (theme) => {
            updateColorTheme(theme);
            log("Updating theme to", theme)
        })
        // Set app theme to match selected theme on load:
        updateColorTheme(app.theme)
    })
    ```

5. Publish your changes to shared.js to your web host.

To test these changes:

1. Open the shared app in a meeting add as a tab to a space. If the shared app is already open in a meeting or space, right-click (or control-click) on any empty area of the shared app's viewport and select **Reload**.

    The app's color theme should match the currently selected theme on initial load.

2. In Meeting Center select **View > Themes** and select a different theme, or in a Webex Space open **Preferences**, click **Appearance** and select a new theme.

    The app's theme changes to match the currently selected theme.

    ![Color theme change test](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4b49e3c1016f8c30/6176f0fdfa86b41ef7469188/color-theme-change.png)
