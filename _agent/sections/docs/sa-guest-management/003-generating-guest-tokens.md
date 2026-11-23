---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sa-guest-management
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Generating Guest Tokens
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sa-guest-management). [Full Markdown](../../../../docs/sa-guest-management.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Guest Management happens via Service Apps in order to provide unlicensed users with temporary access to Webex functionality. 

## Selected section

## Generating Guest Tokens

Once you have created a Service App with `guest-issuer:write` and `guest-issuer:read` scopes in [My Webex Apps](https://developer.webex.com/my-apps), have it approved by a full admin, and have the Service App `Access Token` in hand, you can create guest tokens to authenticate guest users and perform actions against the Webex REST API.

In a single API call to [/guests/token](https://developer.webex.com/admin/docs/api/v1/guest-management/create-a-guest), you can create a guest, refresh the token or switch the guest display name according to the payload supplied.

### Authorization

To authorize your guest creation call, you must use the `Access Token` of the Service App. Remember, the Service App manages the guests. Also, if you want to use the developer portal **Try it** mode, you need to turn off the **Use personal access token** toggle and instead copy the Service App `Access Token` into the **Authorization** field.

### Payload for Guest Creation

To create a guest, you only need to provide two fields in your `POST` [API call](https://developer.webex.com/admin/docs/api/v1/guest-management/create-a-guest). A free-form string identifier that uniquely identifies the guest in your system and a display name shown in Webex Applications, SDKs, and Widgets.

#### POST PAYLOAD

```json
{
  "subject": "My5thPerson",
  "displayName": "King Ralph the 5th"
}
```


#### Response

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8wZmE2NjgwZi01NWIyLTRkYzgtYjAzMC0xZWI0MzI4Y2MxYTg",
  "subject": "My5thPerson",
  "displayName": "King Ralph the 5th",
  "email": "bf2936d4-40b6-3800-8562-5341c9ecc482@appid.ciscospark.com",
  "accessToken": "ACCESS_TOKEN",
  "expiresIn": 64799
}
```

The API response contains the `accessToken` that you use in REST API calls and SDK invocations. The fields are described in detail in the [API reference](https://developer.webex.com/admin/docs/api/v1/guest-management/create-a-guest).

### Using the Access Token

Once you have an access token, you can use it with the Webex REST API to perform actions as the guest user. For example, if your guest user is sending messages to Webex users, use the [Messages API](https://developer.webex.com/docs/api/v1/messages) to send messages to them. The token will include the appropriate scopes for messaging, calling, and people.

For example, you can use the access token to fetch details about the guest user via the [Get My Own Details](https://developer.webex.com/admin/docs/api/v1/people/get-my-own-details) endpoint:

#### Example Request

```bash
curl --request GET \
  --header "Authorization: Bearer ACCESS_TOKEN" \
  https://webexapis.com/v1/people/me
```

#### Example Response

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8yNDAxNjk3NC1kMzEzLTRhNzctOTQ2MS0zYjRhZjU0MjI4OWY",
  "emails": [
    "498fb162-6739-3513-8f68-349ef6359b4f@appid.ciscospark.com"
  ],
  "phoneNumbers": [],
  "displayName": "King Ralph the 4th",
  "nickName": "King",
  "userName": "498fb162-6739-3513-8f68-349ef6359b4f",
  "avatar": "https://avatar-prod-us-east-2.webexcontent.com/default_machine~80",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi83YjhkZDBlMi1kMDU1LTQzNzYtYjgwNC1kZDM4MTYyNDY5YTc",
  "created": "2024-01-30T23:55:27.425Z",
  "status": "unknown",
  "type": "appuser"
}
```

The guest `email` is synthetic and cannot be used to email the guest. The `orgId` is the guest organization ID. All guests are created in their own independent organization.

When using guest access tokens, your application will need to manage guest user sessions. A refresh token is not provided. If a session needs to continue past the expiration time of the access token, create a new guest access token for the user.
