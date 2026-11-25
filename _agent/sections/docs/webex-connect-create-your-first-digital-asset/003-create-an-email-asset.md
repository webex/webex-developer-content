---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-create-your-first-digital-asset
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Create an Email asset
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-create-your-first-digital-asset). [Full Markdown](../../../../docs/webex-connect-create-your-first-digital-asset.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use the Digital Channel Onboarding APIs to programmatically create supported channel assets for your organization.

This guide shows how to try the APIs by creating an Email asset using a personal access token and the corresponding API Reference operation.

## Selected section

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
