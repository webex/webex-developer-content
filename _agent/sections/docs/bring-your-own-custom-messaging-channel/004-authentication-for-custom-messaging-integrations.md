---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Authentication For Custom Messaging Integrations
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel). [Full Markdown](../../../../docs/bring-your-own-custom-messaging-channel.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md) [Attachment URL Requirements](011-attachment-url-requirements.md)

## Article introduction

Connect an external messaging channel to Webex Contact Center through middleware that uses the Custom Messaging APIs.

## Selected section

## Authentication For Custom Messaging Integrations

- For the middleware application to call the Tasks APIs, you must use a [Service App](https://developer.webex.com/docs/service-apps).
- For scope definitions, refer to [Integration Scopes](https://developer.webex.com/docs/integration-scopes).
- The general [Authentication guide](https://developer.webex.com/docs/authentication) explains token acquisition and token refresh behavior.

### Create And Authorize A Service App

1. Sign in to the developer portal and create a new Service App.
1. Capture the client secret when it is first shown. After the app is submitted for authorization, regenerate the secret if it was not saved.
1. Assign the required scopes:
   - `cjp:task_write`
   - `cjp:task_read`
1. Ask the administrator to authorize the Service App in Control Hub under **Apps**.
1. After authorization, return to the Service App in the developer portal, select the authorized organization, provide the client secret, and generate the access token.

Use the resulting access token when calling the Create Task API and the Task Messages API.

For this integration pattern, ensure that:

- The Service App is authorized for the organization
- The access token includes `cjp:task_write` for Create Task and Task Messages
- The access token includes `cjp:task_read` when task read access is required

### Refresh Tokens

For long-running access, retain the refresh token and use the standard OAuth refresh flow described in the [Authentication guide](https://developer.webex.com/docs/authentication#using-the-refresh-token) before the current access token expires.

For server-to-server integrations, store the client secret, access token, and refresh token securely, and rotate or regenerate credentials according to your organization's security practices.
