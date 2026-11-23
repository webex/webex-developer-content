---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-a-fedramp-integration
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Integration API Reference
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-a-fedramp-integration). [Full Markdown](../../../../docs/create-a-fedramp-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Integrations, in contrast to bots, must be authorized by users and act on the user's behalf. During the authorization process the integration requests fine-grained controls which the authorizing user has visibility into. The rolls determine which REST endpoints the integration is allowed to call.

---

Just like bots, a Webex Integration must be created by a FedRAMP Webex Control Hub admin user in the applications file first. In the Webex FedRAMP environment, an integration can only be created via the Webex API. Once the integration is created, an OAuth client ID and secret can be used with an OAuth 2 authorization code flow to obtain an access token. The Integration creation by an admin is a one-time affair for each integration. Once the developer receives the OAuth URL and secret, they can handle user authorizations correctly.

## Selected section

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
