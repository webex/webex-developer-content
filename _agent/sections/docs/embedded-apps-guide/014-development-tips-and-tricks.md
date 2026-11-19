---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Development Tips and Tricks
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

## Development Tips and Tricks

This section provides an assortment of solutions to common questions or problems for developing Embedded Apps.

* [Checking for an Existing Sharing Session](https://developer.webex.com/docs/embedded-apps-guide#check-for-existing-session)
* [Check if App is Running In-Space or In-Meeting](https://developer.webex.com/docs/embedded-apps-guide#check-if-meeting-or-space)
* [Using Cookies and Web Storage](https://developer.webex.com/docs/embedded-apps-guide#cookies_local_storage)
* [About Combined Embedded App and Integration Solutions](https://developer.webex.com/docs/embedded-apps-guide#integrations)
* [Clearing the Webex Cache](https://developer.webex.com/docs/embedded-apps-guide#clear-cache)
* [Ensuring the Framework is Loaded and Ready](https://developer.webex.com/docs/embedded-apps-guide#onready)

<a id="check-for-existing-session"></a>

### Checking for an Existing Sharing Session

It's good practice to check the value of [app.isShared](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+isShared) before calling `setShareUrl()`. This avoids the scenario of the "Open for all" button mistakenly appearing for meeting participants.

For example, in the following code sample the embedded app's `handleSetShare()` is responsible for calling `setShareUrl()` in response to some other event. The function first checks the value of `app.isShared` and exits the function if it's `true`.

```javascript
function handleSetShare(url)
    if (app.isShared) {
      log('ERROR: setShareUrl() should not be called while session is active');
      return;
    }
    // Call setShareUrl() as usual...
}
```

<a id="check-if-meeting-or-space"></a>

### Check if App is Running In-Space or In-Meeting

In some cases an embedded app may need to determine if it's running in a meeting or a space. One way to do this is to check the value of the [app.displayContext](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+displayContext), which contains one of the following values: `"MEETING_SIDEBAR"`, `"MEETING_STANDALONE_WINDOW"`, `"MEETING_MAINVIEW"`, or `"SPACETAB"`. For example, the following code uses the [includes()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes) function to check if `app.displayContext` contains the string "MEETING". If `includes()` returns `true` the app is running in a meeting, otherwise it's running in a space.

```javascript
    var app = new window.Webex.Application();
    var isMeeting = false;

    app.onReady().then(() => {
        // Check if running in a meeting
        isMeeting = app.displayContext.includes("MEETING");
        if(isMeeting) {
            console.log("I'm running in a meeting");
        } else {
            console.log("I'm running in a space");
        }
    }).catch((errorcode) =>  {
        log("Error: ", Webex.Application.ErrorCodes[errorcode]);
    });
```

<a id="cookies_local_storage"></a>

### Using Cookies and Web Storage

Embedded apps can use [cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies) and [Web Storage](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API) the same way they are used in web browsers. Persistent cookies and local storage data are persisted after a user quits the Webex app or Meeting Center client; session cookies and session storage data are deleted when the user closes Webex or Meeting Center.

<a id="integrations"></a>

### About Combined Embedded App and Integration Solutions

Embedded apps can't make [Webex API](https://developer.webex.com/docs/getting-started) calls directly. However, your embedded app can be backed by a server process that acts as a [Webex Integration](https://developer.webex.com/docs/integrations). In this scenario, the embedded app prompts the user to [initiate the OAuth authorization](https://developer.webex.com/docs/integrations#requesting-permission) process to obtain an access token to make Webex API calls on the user's behalf.

First, the user clicks a button or link in the embedded app that opens the Webex authorization request URL(`https://webexapis.com/v1/authorize`). This URL is configured with your Webex integration's [requested scopes](https://developer.webex.com/docs/integrations#scopes), client ID, and redirect URL, and other [request parameters](https://developer.webex.com/docs/integrations#requesting-permission).

![Button to start OAuth flow](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1b0e8e3193410d16/61d8813f9efff26ae759800e/oauth-flow-start.png)

Once the user has signed in to their Webex account they are asked if they want to accept the request for access to data in the specified scopes.

![Webex login screen](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc44413802cdf4f16/61d88843bf9cb8387cc1d960/oauth-flow-login.png)

![User authorizes access to data](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf4cd7db442aeafe7/61d8c28fdbd06039fdcf7ad5/oauth-flow-accept.png)

Once the user accepts the request they are redirected to your integration's specified **Redirect URL**, which is passed an authorization code from the authorization server. This page can [exchange the auth code](https://developer.webex.com/docs/integrations#getting-an-access-token) for an API access token to make Webex API calls (to the [/v1/people/me](https://developer.webex.com/docs/api/v1/people/get-my-own-details) API endpoint, for example) on the user's behalf and display the results in the embedded app, as shown below.

![Redirect page showing results of authenticated API call](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbaea62e45e1e6a40/61d8c29c8b16776549dee779/oauth-flow-authenticated.png)

<a id="clear-cache"></a>

### Clearing the Webex Cache

When iteratively testing changes to your embedded app you'll typically post your changes to your web host, and then click "Reload" in [developer tools menu](https://developer.webex.com/docs/embedded-apps-guide#enabling-developer-tools) to refresh the app. Like stand-alone web browsers the Webex app caches your embedded app's assets for faster loading times, so you may need to clear its cache to view your app's most recent changes.

To manually clear the cache, see the instructions in the following Webex support articles:

* [How Do I Clear the Cache for Webex?](https://help.webex.com/en-US/article/WBX000023766/How-Do-I-Clear-the-Cache-for-Webex) (Windows)
* [How Do I Clear the Webex Cache on a Mac?](https://help.webex.com/en-US/article/WBX000026120/How-Do-I-Clear-the-Webex-Cache-on-a-Mac?)

Alternatively, you can click **Clear Cookies** under the **Accounts** tab in the Webex app's preferences. (Note that this will also log you out of any current Webex sessions.)

![Clear cookies button in Webex preferences](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc0c1d3f1eb9da7b0/61d770c495cb603e6b5ce5c3/webex-clear-cookies.png)

<a id="onready"></a>

### Ensuring the Framework is Loaded and Ready

Once the embedded app framework is loaded and ready to use, it calls your app's `onReady` promise handler, for example:

```javascript
// Create Webex app object and initialize your application
var app = new window.Webex.Application();

app.onReady().then(() => {
    console.log("Framework is ready.");
}
```

However, if this code is parsed and executed before the framework's JavaScript library has finished loading, an 'undefined' runtime error will be generated since the `window.Webex` object doesn't yet exist. To avoid this you can either use the `defer` attribute on the `<script>` tag used to load the framework library, or modify your code to defer creation of the `app` object until `window.Webex` exists. Both of these approaches are described below. An approach for checking for `window.Webex` in a React app is also provided.

* [Using the defer Script Tag Attribute](https://developer.webex.com/docs/embedded-apps-guide#defer-attribute)
* [Wait Until the Webex Object Exists](https://developer.webex.com/docs/embedded-apps-guide#wait-until-the-webex-object-exists)
* [Wait Until the Webex Object Exists in React](https://developer.webex.com/docs/embedded-apps-guide#wait-until-the-webex-object-exists-in-react)

<a id="defer-attribute"></a>

#### Using the defer Script Tag Attribute

When present on a `<script>` tag, the `defer` attribute indicates to the embedded web view in which your app is running that the script should be executed after the document has been parsed. Scripts with the `defer` attribute execute in the order in which they appear in the document. For this reason the `<script>` tag that loads the embedded app framework must be declared before any `<script>` tag that loads your application code, as shown below.

```html
<head>
    <!-- Load the embedded app framework -->
    <script src="https://binaries.webex.com/static-content-pipeline/webex-embedded-app/v1/webex-embedded-app-sdk.js" defer></script>
    <!-- Load your app's main javascript file -->
    <script src="./index.js" defer></script>
</head>
```

With this setup your app's code is guaranteed to execute only after the framework is loaded. Without the `defer` attribute there's a chance that the `window.Webex` object will be `undefined` when your app's code attempts to use it.

<a id="wait-until-the-webex-object-exists"></a>

#### Wait Until the Webex Object Exists

As an alternative to use the `defer` script tag attribute, your app code can defer creation of the main Webex app object until `window.Webex` exists. The framework will then automatically call your `onReady()` promise handler. For example, the following uses the `setInterval()` function before creating the `app` object.

```javascript
// Declare app object:
var app;

// Wait for window.Webex
var checkForWebex = setInterval(function() {
   if (window.Webex) {
      app = new window.Webex.Application();    
   }
}, 100); // check every 100ms

// Define onReady handler:
app.onReady().then(() => {
    console.log("Framework is ready.");
}
```

<a id="wait-until-the-webex-object-exists-in-react"></a>

#### Wait Until the Webex Object Exists in React

The following code demonstrates an approach to checking if the `window.Webex` object is available in a React app using the [Effect hook](https://reactjs.org/docs/hooks-effect.html).

```javascript
const [webexApp, setWebexApp] = useState(false);
useEffect(() => {
  if (webexApp) {
    return;
  }
  const _webexApp = new window.Webex.Application();
  _webexApp.onReady().then(() => {
    console.log("Webex App Ready");
    setWebexApp(_webexApp);
  });
}, [webexApp])
```
