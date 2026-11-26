---
type: Excerpt
canonical_url: https://developer.webex.com/docs/understanding-oauth-flow-of-webex-integration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 3: Exploring the Webex Sample Oauth App Code'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/understanding-oauth-flow-of-webex-integration). [Full Markdown](../../../../docs/understanding-oauth-flow-of-webex-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Step 2: Registering a custom Webex integration](004-step-2-registering-a-custom-webex-integration.md)

## Article introduction

This tutorial demonstrates how to perform Webex OAuth2 authentication for a Webex Integration.

## Selected section

## Step 3: Exploring the Webex Sample Oauth App Code



> **Info**
>
> The complete sample code for this project is available on GitHub: [CiscoDevNet/webex-teams-auth-sample](https://github.com/CiscoDevNet/webex-teams-auth-sample)



Let's take a look at the source code of the sample app, and see how it works:

- Open the sample code on [GitHub](https://github.com/CiscoDevNet/webex-teams-auth-sample/blob/master/webex-teams-auth.html)

To complete the **Webex** authentication sequence, the application performs three main steps:

1. Builds an auth code request URL for the **Webex** OAuth2 `/authorize` service by concatenating your app's registration details, the requested **Webex** API permission scopes, and some other fixed fields.  The app then redirects the browser to the auth code URL, where the user interactively logs in to **Webex**:

    ```javascript
    //Build the request URL.  The base URL and next 4 items are typically always the same for Webex web apps
    var requestUrl = 'https://webexapis.com/v1/authorize?' + //Webex OAuth2 base URL
    'response_type=code&' + // Requesting the OAuth2 'Authentication Code' flow
    'scope='+ encodeURIComponent('spark:rooms_read') + '&' + // Requested permission, i.e. Webex room info
    // The following items are provided by the developer in the source code/config or generated dynamically at run time
    'state=' + encodeURIComponent(randomString(63)) + '&' + // Random string for OAuth2 nonce replay protection
    'client_id=' + encodeURIComponent(appClientId) + '&' + // The custom app Client ID
    'redirect_uri=' + encodeURIComponent(appRedirectUri); // The custom app's Redirect URI
    window.location = requestUrl; // Redirect the browser to the OAuth2 kickoff URL
    ```

    ([view on GitHub](https://github.com/CiscoDevNet/webex-teams-auth-sample/blob/master/webex-teams-auth.html#L33))

2. After **Webex** authenticates the user, the service redirects the browser back to the application's registered **Redirect URI** (in this case, the same URL as the original sample app page) attaching the requested OAuth2 auth code as a URL parameter.  When the page's `window.onload` event fires, it checks for the presence of the auth code URL parameter, and displays it in the 'Auth Code' input field:

    ```javascript
    var params = parseQueryStr(window.location.search.substring(1)); // Parse the query string params into a dictionary
    if (params['code']) { // If the query param 'code' exists, then...
    document.getElementById('code').value = params['code']; // Display the auth code
    document.getElementById('tokenButton').removeAttribute('hidden'); // Reveal the 'Request Access Token' button
    }
    ```

    ([view on GitHub](https://github.com/CiscoDevNet/webex-teams-auth-sample/blob/master/webex-teams-auth.html#L49))

3. Finally, the app creates a JavaScript XMLHttpRequest object, builds a JSON request object (which includes the obtained auth code), the app **Redirect URI**, and some other fixed fields.  It then submits the request to the Webex `/access_token` service to exchange for a **Webex** API access token.  If successful (`xhttp.status == 200`), the access token is displayed in the 'Access Token' field:

    ```javascript
    xhttp = new XMLHttpRequest(); // Create an AJAX HTTP request object
    xhttp.onreadystatechange = function() {  // Define a handler, which fires when the request completes
    if (xhttp.readyState == 4) { // If the request state = 4 (completed)...
    if (xhttp.status == 200) { // And the status = 200 (OK), then...
    var authInfo = JSON.parse(xhttp.responseText); // Parse the JSON response into an object
    document.getElementById('token').value = authInfo['access_token']; // Retrieve the access_token field, and display it
    } else alert('Error requesting access token: ' + xhttp.statusText)
    }
    }
    xhttp.open('POST', 'https://webexapis.com/v1/access_token', true); // Initialize the HTTP request object for POST to the access token URL
    // Build the HTML form request body
    var body = 'grant_type=authorization_code&'+  // This is an OAuth2 Authorization Code request
    'redirect_uri='+encodeURIComponent(appRedirectUri)+'&'+ // Same custom app Redirect URI
    'code='+encodeURIComponent(document.getElementById('code').value)+'&'+ // User auth code retrieved previously
    'client_id='+encodeURIComponent(appClientId)+'&'+ // The custom app Client ID
    'client_secret='+encodeURIComponent(appClientSecret); // The custom app Client Secret
    xhttp.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded'); // Sending the content as URL-encoded form data
    xhttp.send(body); // Execute the AJAX HTTP request
    ```

    ([view on GitHub](https://github.com/CiscoDevNet/webex-teams-auth-sample/blob/master/webex-teams-auth.html#L66))
