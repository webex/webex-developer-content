---
type: Excerpt
canonical_url: https://developer.webex.com/docs/understanding-oauth-flow-of-webex-integration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 5: Check your work'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/understanding-oauth-flow-of-webex-integration). [Full Markdown](../../../../docs/understanding-oauth-flow-of-webex-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Step 2: Registering a custom Webex integration](004-step-2-registering-a-custom-webex-integration.md)

## Article introduction

This tutorial demonstrates how to perform Webex OAuth2 authentication for a Webex Integration.

## Selected section

## Step 5: Check your work

Let's take the access token you just retrieved and test it using the **Webex** interactive documentation to see if it is working as expected.  You can use this [note-box page](https://developer.cisco.com/learning/posts/files/collab-webex-auth/notebox.html) to copy/paste the access token from the sample app form into temporarily.

**1)** Use the access token to list your **Webex** rooms.

- Navigate to the **Webex** interactive documentation page for [**List Rooms**](https://developer.webex.com/docs/api/v1/rooms/list-rooms).
- Make sure you are logged in, and have the Try it button enabled ![Try it](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4281a6566d5258b5/61fc1ad72632163e756da5f9/try_mode.png).
- In the **Headers** section, view the `Authorization` field.  This field contains the string `Bearer`, a space, and then an access token.  By default, the field is pre-populated with your personal developer token based on your login.  In this case, we want to replace that default token with the access token generated using the OAuth sample app.  

- Toggle **Use personal access token** to clear the pre-populated access token.
![Authorization header](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt478aed7d3bf1da9b/61fb08845865427ee15b8fed/bearer.png)

- Paste the access token from Step 4 after the word `Bearer`, followed by a space (be sure and preserve capitalization and the space after `Bearer`).

- Click ![Run button to execute the request](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt039fe43fb24253c2/61fb097d7ece8a1a37f71a98/run.png)

- **Results:** If all went well, in the response output window you should see a `Response 200/OK` result, and a JSON-format array of room details:
    ![Success](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf610a76f041c9e77/61fb0a91d970ea1bb42ad768/success.png)

**2)** Try to access data from the **Webex** `/people/me` resource

- Visit the **Webex** interactive documentation page for **Get My Own Details** for ['me'](https://developer.webex.com/docs/api/v1/people/get-my-own-details), i.e. the user associated with the access token

- As above, toggle **Use personal access token** to clear the pre-populated access token, and paste the access token obtained via the sample app.

- Click ![Run](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt039fe43fb24253c2/61fb097d7ece8a1a37f71a98/run.png)

- **Results:** In this test, the expected result is actually a failure response, i.e. a `Response 403/Forbidden` message:
    ![Unauthorized](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1c2e980dbc3d05d8/61fb0c1addbb853fe258bda6/unauthorized.png)



> **Info**
>
> A 'Forbidden' result is expected here, because when the sample app obtained its access token from the **Webex** service, it only requested the `spark:rooms_read` authorization scope.  This means that the access token returned by **Webex** will only allow read (**GET**) requests from the `/rooms` API resource.  As the test above attempts to read info from the `/people` resource, the request is rejected.



If desired, the sample app could be updated to also include the `spark:people_read` scope to allow making API requests for the `/people` resource by updating this line of code:

```javascript
'scope='+ encodeURIComponent('spark:rooms_read spark:people_read') + '&' +
```

([view on GitHub](https://github.com/CiscoDevNet/webex-teams-auth-sample/blob/master/webex-teams-auth.html#L36))
