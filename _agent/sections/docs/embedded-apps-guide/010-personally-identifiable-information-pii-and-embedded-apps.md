---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Personally Identifiable Information (PII) and Embedded Apps
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

## Personally Identifiable Information (PII) and Embedded Apps

The Embedded App framework provides APIs that may return personally identifiable information (PII) about its users, but only if permitted by the Webex organization’s administrator. Access to a user's personal data for a given app is determined by the **PII Restrictions** setting specified in [Control Hub](https://admin.webex.com) by the administrator of the user's Webex organization.

* [PII Data Provided by the Embedded Apps SDK](https://developer.webex.com/docs/embedded-apps-guide#pii-data-provided-by-the-embedded-apps-sdk)
* [Determining if Personal Data is Available](https://developer.webex.com/docs/embedded-apps-guide#is-private-data-available)
* [In-Development Apps and PII](https://developer.webex.com/docs/embedded-apps-guide#in-development-apps)
* [About Derived Values](https://developer.webex.com/docs/embedded-apps-guide#about-dervied-pii-values)
* [About the JSON Web Token (JWT)](https://developer.webex.com/docs/embedded-apps-guide#about-the-json-web-token)
* [Verifying a JWT](https://developer.webex.com/docs/embedded-apps-guide#verifying-the-jwt)
* [JWT field reference](https://developer.webex.com/docs/embedded-apps-guide#jwt-field-reference)

<a id="pii-data-provided-by-the-embedded-apps-sdk"></a>

### Personally Identifiable Information Returned by the SDK

The following data fields may contain personally identifiable information (PII) if access to PII has been granted to the app by the organization administrator (see [Determining if Personal Data is Available](https://developer.webex.com/docs/embedded-apps-guide#is-private-data-available)).

* User data returned by [app.context.getUser()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application.Context+getUser):

  * User ID (`user.id`)
  * User Email (`user.email`)
  * User Display name (`user.displayName`)
  * User Organization ID (`user.orgId`)

* Meeting data returned by [app.context.getMeeting()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application.Context+getMeeting):

  * Meeting Conference ID (`meeting.conferenceId`)
  * Meeting ID (`meeting.id`)
  * Meeting Title (`meeting.title`)

* Messaging space data returned by [app.context.getSpace()](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application.Context+getSpace):

  * Space ID (`space.id`)
  * Space Title (`meeting.title`)

In addition, the [JSON Web Token (JWT)](../../../../docs/(/docs/embedded-apps-guide#about-the-json-web-token)) included in the response to `getUser()` contains the following additional PII:

* Conference ID (`com.cisco.context.uuid.conferenceid`)

<a id="is-private-data-available"></a>

### Determining if Personal Data is Available

An embedded app can determine if it has access to the given user's personal data by checking the value of [app.isPrivateDataAvailable](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+isPrivateDataAvailable). If this property is `true` then data returned by API calls such as `app.context.getUser()` will contain real values; if `false`, data returned by the SDK will contain either empty strings or "derived" values. Derived values are opaque to third-parties but are guaranteed to be consistent for a given user from a given Webex organization. See [About Derived PII Values](https://developer.webex.com/docs/embedded-apps#about-derived-pii-values) for more information.

If an app is being shared among users from multiple Webex organizations, `app.isPrivateDataAvailable` will be `true` for those users from organizations that have approved access to personal data for that app, and `false` for users from organizations that have not. In this case, embedded app APIs will return actual data for some users and derived data for others.

For apps that haven't yet been approved for use by an organization administrator, individual app users determine if they want to share their personal data. See [In-Development (Private) Apps and Personal Data](https://developer.webex.com/docs/embedded-apps-guide#in-development-apps) for more information.

<a id="in-development-apps"></a>

### In-Development Apps and PII

By default, embedded apps appear in the Apps Gallery only for the user who created the app in the Developer Portal. These apps are referred to as being "in-development". To make an in-development app available to all users within an organization an administrator must [approve the app](https://help.webex.com/en-us/article/y1eqyd/Embedded-apps-in-Webex#Cisco_Task_in_List_GUI.dita_embeddedapp1) in Webex [Control Hub](https://admin.webex.com).

If an unapproved app is shared by the app creator with other users via the **Open for all** or **Add to Space** functionality, users are asked before they can open the shared content if they want to share their personally identifiable information with the app or not, as shown below.

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3cd8bceeba599606/616f513399dfaf274905b415/warning_pii.png" alt="In-development PII warning dialog" style="width: 50%;"></img>

In this case the value of `app.isPrivateDataAvailable` will be determined by which option the user selected before opening the app.

<a id="about-dervied-pii-values"></a>

### About Derived PII Values

If an organization has disabled access to personally identifying information for a given application (i.e. if `app.isPrivateDataAvailable` is `false`) then any fields that would normally contain PII will either contain empty strings or "derived" values. Derived values are opaque to third-parties but are guaranteed to be consistent for a given user from a given organization. This allows apps to uniquely identify their users even if they don't have access to PII.

For example, the following shows an example [User](https://developer.webex.com/docs/embedded-apps-api-reference#User) object returned by `app.context.getUser()` when access `app.isPrivateDataAvailable` is `true`.

```javascript
{
    "id": "c9d03fc2-a5e4-452f-bed1-aa1ede630666",
    "orgId": "38adfc99-2313-402c-a913-d68a6536f7df",
    "email": "user@example.com",
    "displayName": "Joe User",
    "token": "<encoded_JWT>"
}
```

The following is an example [User](https://developer.webex.com/docs/embedded-apps-api-reference#User) object when `app.isPrivateDataAvailable` is false for a user of the same app. In this case the `email` and `displayName` fields are empty, while `id` and `orgId` contain derived UUIDs instead of real values.

```javascript
{
    "id": "833c49ff-9a88-4c2c-af13-6fc30cb2223a",
    "orgId": "c4baee52-d3ba-4329-ac44-40bac96853c5",
    "email": "",
    "displayName": "",
    "token": "<encoded_JWT>"
}
```

If a meeting or space has a mix of participants – some with access to PII enabled and some who do not – there will be two different IDs. Users with PII enabled will have the real meeting (or space) ID in the `meeting.id` or `space.id` field, while users without PII enabled will have derived IDs for those fields.

<a id="about-the-json-web-token"></a>

### About the JSON Web Token (JWT)

The `User` object returned by `app.context.getUser()` contains a field named `token` whose value is a Base64-encoded JSON structure, called a [JSON Web Token](https://jwt.io/introduction), or JWT.

```json
{
    "id": "...",
    "orgId": "...",
    "email": "...",
    "displayName": "...",
    "token": "eyJhbGciOiJSUzI1NiJ9..."
}
```

The purpose of the JWT in the context of embedded apps is two-fold:

* Provide a way for embedded apps to verify the integrity of the data they are provided by the framework. See [Verifying the JWT](https://developer.webex.com/docs/embedded-apps-guide#verifying-the-jwt) for details.
* Expose additional data fields to apps beyond what are available as top-level API properties. See [JWT field reference](https://developer.webex.com/docs/embedded-apps-guide#jwt-field-reference) for a list of all data fields contained by the JWT.



> **Info**
>
> The JWT is **not** an access token for calling Webex APIs on behalf of the user of your application. Your applications will need to obtain an access token following the standard [integration workflows](https://developer.webex.com/docs/integrations).



<a id="verifying-the-jwt"></a>

### Verifying the JWT

To verify the authenticity of the JWT token returned by `getUser()` you need to obtain the verification key at a URL provided by Webex. To obtain this URL you concatenate the base URL contained by the `iss` (issuer) field in the decoded JWT with the string **/oauth2/v2/keys/verification**. The verification key is contained by the `new_verification_key` field of the JSON object returned at this URL.

For example, the following shows a decoded JWT whose `iss` field contains the URL `https://idbroker-b-us.webex.com/idb`.

```json
{
  "email_verified": false,
  "iss": "https://idbroker-b-us.webex.com/idb",
  ...
}
```

Therefore, the full URL to obtain the verification key in this scenario would be <https://idbroker-b-us.webex.com/idb/oauth2/v2/keys/verification>. Below is an example JSON object containing the `new_verification_key` field returned by the full verification URL:

```json
{
    key_valid_time: 21600,
    new_verification_key: "MIIBIjANBgk..."
}
```



> **Warning**
>
> To avoid any potential "man-in-the-middle" security threat, developers are encouraged to verify that the base URL specified by the `iss` field contains the **webex.com** domain before using it to verify the JWT.



<a id="jwt-field-reference"></a>

### JWT field reference

The section lists the fields of the JWT returned in response to a call to `app.context.getUser()`. Some of these fields are also available on the `User` object returned by `getUser()`, such as `user.id` or `user.email`. Others are only available as JWT fields, such as `given_name`.

The following are registered claim names included in the JWT:

* `exp` – Number. Life span of token in seconds.
* `iat` – Number. The time the token was issued.
* `iss` – String. URI of the principal that issued the claims contained by the token (<https://idbroker.webex.com/idb>, for example)
* `aud` – String. ID of embedded application.
* `name` – String. User’s display name. Empty if access to PII has been disabled by the user's organization.
* `given_name` – String. User’s first name. Empty if access to PII has been disabled by the user's organization.
* `family_name` – String. User’s last name. Empty if access to PII has been disabled by the user's organization.
* `email` – String. User's email.  Empty if access to PII has been disabled by the user's organization.
* `email_verified` – Boolean. If "true" indicates that the email was verified by Cisco and the user's PII is shared in the token. If "false", indicates that the user's email was not verified by Cisco and derived values are used for PII.

The following are Cisco claim names included in the JWT:

* `com.cisco.user.orgid` – String. User's organization ID. Contains a derived value if access to PII is disabled for the app by the organization administrator.
* `com.cisco.user.uuid` – String. User ID. Contains a derived value if access to PII is disabled for the app by the organization administrator.
* `com.cisco.user.level` – Array. Contains one or more of the following values:
  * "admin"
  * "guest"
  * "basic"
  * "enhanced"
* `com.cisco.context.uuid.conferenceid` – String. Conference ID. Contains a derived value if access to PII is disabled for the app by the organization administrator.
* `com.cisco.context.uuid.conferenceid.`derived – String. Derived conference ID. If access to PII is disabled for the app by the organization administrator this will match the value of com.cisco.context.uuid.conferenceid.
* `com.cisco.context.uuid.meetingid` – String. Meeting ID. Contains a derived value if access to PII is disabled for the app by the organization administrator.
* `com.cisco.context.uuid.meetingid.derived` – String. Derived meeting ID. If access to PII is disabled for the app by the organization administrator this will match the value of `com.cisco.context.uuid.meetingid.`
* `com.cisco.context.uuid.spaceid` – String. Space ID. Contains a derived value if access to PII is disabled for the app by the organization administrator.
* `com.cisco.context.uuid.spaceid.derived` – String. Derived space ID. If access to PII is disabled for the app by the organization administrator this will match the value of com.cisco.context.uuid.spaceid.
* `com.cisco.user.info` – JSON blob containing additional information about the user, meeting, or space.

Below is an example JWT returned by a call to `app.context.getUser()`, using abbreviated UUIDs for clarity. In this case, `email_verified` is false which indicates that derived or empty values are returned in place of PII (see [About Derived PII Values](https://developer.webex.com/docs/embedded-apps-guide#about-dervied-pii-values) for details on when derived or empty values are returned).

```javascript
{
  "email_verified": false,
  "iss": "https://idbroker-b-us.webex.com/idb",
  "com.cisco.context.uuid.meetingid.derived": "a9b68195-...",
  "com.cisco.user.uuid": "bbd582d2-...",
  "com.cisco.context.uuid.meetingid": "a9b68195-...",
  "com.cisco.context.uuid.conferenceid": "55c205d8-...",
  "given_name": "",
  "aud": "Y2lzY29z...",
  "com.cisco.user.orgid": "86434df5-...",
  "com.cisco.context.uuid.conferenceid.derived": "55c205d8-...",
  "name": "",
  "com.cisco.user.level": [
    "enhanced",
    "admin"
  ],
  "exp": 1634679561,
  "iat": 1634593161,
  "family_name": "",
  "email": "",
  "com.cisco.user.info": "{\"some_property_name\":\"Some data.\"}"
}
```
