---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-issuer
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Using Guest Tokens
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guest-issuer). [Full Markdown](../../../../docs/guest-issuer.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Guest Issuer applications give guest users temporary access to users within your organization. Guest Issuer app creation has been removed—use [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) for new integrations, or follow [Guest Issuer Migration Guide](https://developer.webex.com/docs/guest-issuer-migration) if you have an existing legacy issuer.

## Selected section

## Using Guest Tokens

Once you've created a guest token, you can use it to authenticate as a guest user and interact with Webex users. Several functions in the Webex SDKs can be performed after authenticating with a guest token. If you need to use the Webex REST API directly, you'll need to exchange it for an access token. See below for a few examples of using a guest token with our SDKs and the API.

After a guest user is authenticated, a Webex guest account is created, and they can then perform actions just like regular users. There are a few important differences from regular users to keep in mind:

- Webex accounts for guest users are created only after authenticating with a guest token; accounts cannot be created manually
- Guest users may only interact with regular users; they cannot interact with other guest users
- Guest users will not have a valid email address associated with their account—use their individual `personId` with any activities that require the identification of a specific user

When using guest tokens with the SDKs and Widgets, session management is handled automatically. If the guest token is exchanged for an access token, your application will need to handle guest user sessions. See _Using the Access Token_ below for more information.

### Using with the Browser SDK

The [Browser SDK](https://developer.webex.com/docs/sdks/browser) accepts guest tokens when authorizing a user. To initialize and authenticate with a guest token instead of using a grant flow, use the `requestAccessTokenFromJwt` function. The function's input is an object with a property of "jwt" that's set to a valid guest token. For example, `{jwt: "your.guest.token.here"}`. This function exchanges the guest token for an access token and authenticates the session using that access token.

```javascript
var Webex = require('webex');
var webex = Webex.init();

var token = 'your.guest.token.here';
// wait until the SDK is loaded and ready
webex.once(`ready`, function() {
    webex.authorization.requestAccessTokenFromJwt({jwt: token})
      .then(() => {
        // the user is now authenticated with a guest token (JWT)
        // proceed with your app logic
      })
});
```

### Using with the iOS SDK

To initialize and authenticate the [iOS SDK](https://developer.webex.com/docs/sdks/ios) with a guest token, provide it as a parameter when authorizing the user:

```swift
let authenticator = JWTAuthenticator()
let spark = Spark(authenticator: authenticator)

if !authenticator.authorized {
    authenticator.authorizedWith(jwt: myJwt)
}
```

### Using with the Widgets

To use the [Widgets](https://developer.webex.com/docs/widgets) with a guest token, simply instantiate the widgets with a guest token. For example, here's how you would use a guest token with the [Space Widget](https://developer.webex.com/docs/widgets#space-widget):

```javascript
var widgetEl = document.getElementById('my-webexteams-widget');
// Init a new widget
webex.widget(widgetEl).spaceWidget({
  guestToken: 'GUEST_TOKEN',
  destinationId: 'SPACE_ID',
  destinationType: 'spaceId'
});
```

To quickly test a guest token with the widgets, use the [Widgets Demo](https://code.s4d.io/widget-demo/production/index.html).

### Exchanging for an Access Token

The SDKs handle the guest token exchange and authentication for you, but if you aren't using an SDK, or need more control over the authentication process, you can use the REST API to exchange a guest token for an access token. You can then use the access token to make API requests like you would with a bot token or integration token.

To exchange the guest token for an access token, make an HTTP POST to a special endpoint with the guest token in the `Authorization` header:

#### Example Request

```bash
curl --request POST \
  --header "Authorization: Bearer GUEST_TOKEN" \
  https://webexapis.com/v1/jwt/login
```

You will then receive the access token and an expiration time in seconds:

#### Example Response

```json
{
  "token": "ACCESS_TOKEN",
  "expiresIn": "21599"
}
```

In this example, the access token will be valid for almost six hours. The expiration (`exp`) claim in the guest token will not affect this expiration time.

### Using the Access Token

Once you have an access token, you can use it with the Webex REST API to perform actions as the guest user. For example, if your guest user is sending messages to Webex users, use the [Messages API](https://developer.webex.com/docs/api/v1/messages) to send messages to them. The token will include the appropriate scopes for messaging, calling, and people.

When using access tokens, your application will need to manage guest user sessions. A refresh token is not provided after exchanging the guest token for an access token. If a session needs to continue past the expiration time of the access token, create a new guest token for the user and exchange it for a new access token.

For example, you can use the access token to fetch details about the guest user via the [Get My Own Details](https://developer.webex.com/docs/api/v1/people/get-my-own-details) endpoint:

#### Example Request

```bash
curl --request GET \
  --header "Authorization: Bearer ACCESS_TOKEN" \
  https://webexapis.com/v1/people/me
```

#### Example Response

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8wMDAwMDAwMC0xMTExLTIyMjItMzMzMy00NDQ0NDQ0NDQ0NDQ",
  "emails": [
    "00000000-1111-2222-3333-444444444444@appid.ciscospark.com"
  ],
  "phoneNumbers": [],
  "displayName": "Guest User",
  "nickName": "Guest",
  "avatar": "https://00792fd90955bc2b54b7-dde9bcd8a491bb35da928cc2123a400b.ssl.cf1.rackcdn.com/default_machine~80",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8wMDAwMDAwMC0xMTExLTIyMjItMzMzMy00NDQ0NDQ0NDQ0NDQ",
  "created": "2019-10-01T15:00:00.000Z",
  "status": "unknown",
  "type": "appuser"
}
```

### Changing the Display Name

To change the display name of a guest user who has already authenticated, simply re-authenticate with a new guest token. Create a new guest token and change the `name` payload claim to the new display name. To ensure that this new guest token is associated with the same guest user, use the same unique user identification value for the `sub` payload claim. After authenticating via the API or with the SDKs with the new guest token, the guest user's display name will be updated.
