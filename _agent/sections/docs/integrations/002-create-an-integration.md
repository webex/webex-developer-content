---
type: Excerpt
canonical_url: https://developer.webex.com/docs/integrations
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Create an integration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/integrations). [Full Markdown](../../../../docs/integrations.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Webex Contact Center requirements](003-webex-contact-center-requirements.md) [Scopes](004-scopes.md)

## Article introduction

Create a Webex integration when your application needs a user to authorize access to Webex APIs on their behalf.

[Create an Integration](<https://developer.webex.com/my-apps/new/integration>)

## Selected section

## Create an integration

1. Sign in and open [My Webex Apps](https://developer.webex.com/my-apps).
2. Select **Create a New App**, then select **Create an Integration**.
3. Enter a user-facing name and description, and add an icon.
4. Add each redirect URI that your application can use for the OAuth callback.
5. Select only the [integration scopes](https://developer.webex.com/docs/integration-scopes) required by your application.
6. Save the integration and copy its client ID and client secret.

The client secret is shown only when the integration is created. Store it securely and never expose it in browser or mobile application code.



> **Info**
>
> Each Webex user account is limited to 20 integrations.
