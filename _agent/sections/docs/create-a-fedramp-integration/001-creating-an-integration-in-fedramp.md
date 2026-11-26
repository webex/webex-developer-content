---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-a-fedramp-integration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Creating an Integration in FedRAMP
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-a-fedramp-integration). [Full Markdown](../../../../docs/create-a-fedramp-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Integrations, in contrast to bots, must be authorized by users and act on the user's behalf. During the authorization process the integration requests fine-grained controls which the authorizing user has visibility into. The rolls determine which REST endpoints the integration is allowed to call.

---

Just like bots, a Webex Integration must be created by a FedRAMP Webex Control Hub admin user in the applications file first. In the Webex FedRAMP environment, an integration can only be created via the Webex API. Once the integration is created, an OAuth client ID and secret can be used with an OAuth 2 authorization code flow to obtain an access token. The Integration creation by an admin is a one-time affair for each integration. Once the developer receives the OAuth URL and secret, they can handle user authorizations correctly.

## Selected section

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
