---
type: Guide
title: Create a FedRAMP Integration | Consolidated Guide
display_title: Create an Integration
canonical_url: https://developer.webex.com/docs/create-a-fedramp-integration
content_type: documentation
product_group:
- webex-suite
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/create-a-fedramp-integration)

Integrations, in contrast to bots, must be authorized by users and act on the user's behalf. During the authorization process the integration requests fine-grained controls which the authorizing user has visibility into. The rolls determine which REST endpoints the integration is allowed to call.

---

Just like bots, a Webex Integration must be created by a FedRAMP Webex Control Hub admin user in the applications file first. In the Webex FedRAMP environment, an integration can only be created via the Webex API. Once the integration is created, an OAuth client ID and secret can be used with an OAuth 2 authorization code flow to obtain an access token. The Integration creation by an admin is a one-time affair for each integration. Once the developer receives the OAuth URL and secret, they can handle user authorizations correctly.

## Creating an Integration in FedRAMP

First the admin must retrieve their access token from the control hub environment as described above. Admin tokens are valid for no longer than 12 hours. The admin, using the access token, creates a new integration by sending a POST request to the Applications API (see Applications API Reference later in this document for more details) with a tool like Postman or the cURL command line tool. This is no different than bot creation aside from the payload now identifying an integration.

### Example Request

```bash
POST https://api-usgov.webex.com/v1/applications
```

Include the access token in an Authorization header with “`Authorization: Bearer YOUR_TOKEN_FROM_ABOVE`”, and a `Content-Type of application/json`.

Include the

- Type
- Name
- Description
- Contact email
- Redirect URLs for authentication
- Necessary scopes.

The OAuth client ID and client secret will be included in the response. This is the only time you will see the client secret. Store it in a safe place as your developers will need it in the OAuth2 authorization flow.

### Example Headers

```json
Authorization: Bearer <your token>
Content-Type:application/json
```

### Example Request Body

```json
{
  "type":"integration",
  "name":"My Admin Integration",
  "description":"A brief description of the app",
  "contactEmail": "myEmail@example.com",
  "companyName":"My Company",
  "redirectUrls":["https://my-application.example.com/"],
  "scopes": ["audit:events_read"]
}
```

### Example Response Body

```bash
{
  "isNative":false,
  "id":"Y2lzYmNiNTE2YzA1NmZhYmJiOTA5NWM3MWQ2Y2JjZWRjYTYwNmJh",
  "friendlyId": "my-app-1234","type":"integration",
  "name":"My Admin Integration",
  "description":"A brief description of the app",
  "orgId":"Y2lzY29zcGFyazowNGVkLTRlZGUtYWI3ZC1iNWRiNDYyYjgzMzM",
  "contactEmail":"myEmail@example.com",
  "companyName": "My Company",
  "redirectUrls":["https://my-application.example.com/"],
  "scopes": ["audit:events_read"],
  "clientId": "Cd3e3f3d9576dca606ba",
  "clientSecret":"06feae95907defef0a45c",
  "isFeatured":false,
  "submissionStatus":"none",
  "createdBy": "Y2lzY29zcGFyaEtYjY0MS1lZTdiYTI5MWYyM2Y",
  "created":"2020-02-29T21:40:51.150Z"
}
```

Use the OAuth ClientID and Client Secret with your application.

## Using the Integration in FedRAMP

See the Requesting Permission section of the Integrations guide on the Webex for Developers site (<https://developer.webex.com/docs/integrations#requesting-permission>) for detailed instructions on how to use an integration.

Use <https://api-usgov.webex.com/v1/authorize> for the authorization URL and <https://api-usgov.webex.com/v1/access_token> for the access token URL.

Once your application is authorized by a full admin, a new access token and a refresh token are generated and can be used with the authorized Webex REST APIs. An access token is valid for 14 days and can be refreshed using the refresh token which is valid for 60 days. Creating a new access token refreshes the refresh token expiration timer.

## Integration API Reference

### Method

```bash
POST https://api-usgov.webex.com/v1/applications
```

### Request Parameters



| Name | Type | Description | Required |
| --- | --- | --- | --- |
| type | string | The type of application. Use integration. | Y |
| name | string | A brief name for the application. | Y |
| description | string | A brief description for the application. | Y |
| contactEmail | string | The email address of the application developer. | Y |
| redirectURLs | array[string] | An array of redirect URLs for the integration. These URLs will be used after authenticating the user. | Y |
| scopes | array[string] | An array of OAuth scopes required by the application. See Scopes for more information <https://developer.webex.com/docs/integrations#scopes>. | Y |

### Example Request Body

```json
{
  "type":"integration",
  "name":"My Admin Integration",
  "description":"A brief description of the app",
  "contactEmail": "myEmail@example.com</a>",
  "companyName":"MyCompany",
  "redirectUrls":["https://my-application.example.com/"],
  "scopes": ["audit:events_read"]
}
```

### Example Response Body

```json
{
  "isNative":false,
  "id":"Y2lzYmNiNTE2YzA1NmZhYmJiOTA5NWM3MWQ2Y2JjZWRjYTYwNmJh",
  "friendlyId": "my-app-1234",
  "type":"integration",
  "name":"My Admin Integration",
  "description":"A briefd escription of the app",
  "orgId":"Y2lzY29zcGFyazowNGVkLTRlZGUtYWI3ZC1iNWRiNDYyYjgzMzM",
  "contactEmail":"myEmail@example.com",
  "companyName":"My Company","redirectUrls":["https://my-application.example.com/"],
  "scopes": ["audit:events_read"],
  "clientId": "Cd3e3f3d9576dca606ba",
  "clientSecret":"06feae95907defef0a45c",
  "isFeatured":false,
  "submissionStatus":"none",
  "createdBy":"Y2lzY29zcGFyaEtYjY0MS1lZTdiYTI5MWYyM2Y",
  "created":"2020-02-29T21:40:51.150Z"
}
```

A successful request will return `HTTP 200 OK`.
