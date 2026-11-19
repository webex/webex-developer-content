---
type: Guide
title: Create Your First Webex Connect Digital Asset
display_title: Create Your First Digital Asset
canonical_url: https://developer.webex.com/docs/webex-connect-create-your-first-digital-asset
content_type: documentation
product_group:
- webex-connect
categories:
- webex-connect
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-connect-create-your-first-digital-asset)

Use the Digital Channel Onboarding APIs to programmatically create supported channel assets for your organization.

This guide shows how to try the APIs by creating an Email asset using a personal access token and the corresponding API Reference operation.

## Before you begin

You need:

- A Webex Connect organization and its organization ID;
- A Webex user with permission to manage digital assets;
- A personal access token containing the required digital asset scope;
- The configuration required by the selected asset type; and
- The Digital Channel Onboarding API base URL for your region. See [API Endpoints and Regions](https://developer.webex.com/docs/webex-connect-api-endpoints-and-regions).

## Choose an asset type

| Asset type | Configuration to prepare |
|---|---|
| Email | Asset details and the required mailbox, SMTP, and OAuth 2.0 configuration. |
| Chat | Asset details and the configuration for Push Notifications, Live Chat, or In-App Messaging defined by the operation. |

Use the request schema and example provided for the selected asset. Do not copy channel-specific fields from a different asset type.

## Create an Email asset

The Email create operation uses `POST /v2/digital/app` with `channel=email`.

```bash
curl --request POST \
  --url '<digital-asset-api-base-url>/v2/digital/app?channel=email' \
  --header 'Authorization: Bearer <personal-access-token>' \
  --header 'x-organization-id: <organization-id>' \
  --header 'trackingid: <unique-tracking-id>' \
  --header 'Content-Type: application/json' \
  --data '{
    "assetName": "Customer Support Email",
    "assignedTo": "cpaas",
    "description": "Email asset for customer support",
    "flowCanvas": "connect",
    "email": {
      "emailConfig": {
        "accountConfig": {
          "emailId": "<email-id>",
          "emailAddress": "<mailbox-address>",
          "authenticationType": "oauth2",
          "server": "<smtp-server>",
          "port": 587
        },
        "oAuthConfig": {
          "authorizationConfiguration": {
            "clientId": "<oauth-client-id>",
            "clientSecret": "<oauth-client-secret>",
            "grantType": "authorization_code",
            "authUrl": "<authorization-url>",
            "scope": "<mail-provider-scopes>",
            "accessTokenUrl": "<access-token-url>"
          }
        }
      }
    }
  }'
```

The complete Email schema can require additional fields. Use the API Reference as the source of truth before running the request.

## Review the response

A successful operation returns `200 OK` and can include `assetDetails` together with `code`, `description`, and `transid`. Save the asset identifier and transaction ID needed for later retrieval or troubleshooting.

If the request fails:

- use `400` details to correct the query, header, or body;
- obtain a current token for `401`;
- verify the asset scope, organization access, and user permission for `403`; or
- retain `transid` and `trackingid` when reporting a `500` error.

## Create a Chat asset

Open the corresponding Chat asset create operation in the Digital Asset API Reference and repeat the same access pattern with that operation's request schema. Chat assets support Push Notifications, Live Chat, and In-App Messaging; use the exact configuration required by the selected operation. The personal access token, organization header, and authorization checks remain the same.

## Next steps

- Retrieve the asset to confirm its saved configuration and status.
- Update the asset using the exact update operation for its channel.
- Review [Status and Error Codes](https://developer.webex.com/docs/webex-connect-status-and-error-codes) and [Troubleshooting APIs](https://developer.webex.com/docs/webex-connect-troubleshooting-apis).
