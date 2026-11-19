---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspace-integration-technical-details
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Security
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/workspace-integration-technical-details). [Full Markdown](../../../../docs/workspace-integration-technical-details.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide describes the technical details and syntax for the manifest, OAuth, and notification messages.

---

Follow the steps below to set up a new `org_private` Workspace Integration. Every step is detailed further below in this guide.

1. Describe the application in a manifest file and upload it in Control Hub. This gives you an OAuth client ID and a client secret. For further details, see [The Integration Manifest](https://developer.webex.com/docs/workspace-integration-technical-details#the-integration-manifest) for information regarding the manifest, and [Deployment](https://developer.webex.com/docs/workspace-integration-technical-details#deployment) to make the integration available for customers to activate.
2. Receive an activation JWT. If the manifest specified the manual provisioning flow, this happens by an admin activating the integration in Control Hub and copy-pasting the JWT to your integration, as described in [Activation](https://developer.webex.com/docs/workspace-integration-technical-details#activation).
3. Use the OAuth credentials from step 1 and the credentials from step 2 to update the integration status, as described in step 4 of [Activation](https://developer.webex.com/docs/workspace-integration-technical-details#activation).

    At this point, you have everything you need to start interacting with the Webex APIs.

4. Implement the rest of the Workspace Integrations protocol.
5. Use your credentials to interact with the Webex APIs in order to implement your functionality.

To create a _public_ integration there are some additional steps, such as that the manifest needs to be approved and deployed by Cisco, as detailed in the sections below.



> **Info**
>
> Analytics, Meeting and XSI scopes do not currently work with Workspace Integrations.

## Selected section

## Security

Security is very important to Cisco and our customers and it's crucial that integrators focus on security when writing the integration.
Please have a look at the following security guidelines as you plan and review the implementation of your integration:



| Item | Description  |
| ---- | ------------ |
| Validate all JSON Web Tokens (JWT) | Make sure to verify the signature of the JWT and reject any JWTs where the `jti` (ID) has been seen before or where the `appId` does not match the appId provided by the integration in the manifest. In the case of the activation JWT (action: provision), reject any JWT where the `expiryTime` has passed. For any other JWT action type, an `iat` older than 5 minutes should be rejected. |
| Validate webhook authenticity | HMAC verification is the preferred authentication strategy. Always compute the HMAC-SHA1 for the webhook payload and assert that it is the same as the provided `X-Spark-Signature` HTTP header, or verify the contents of the `Authorization` header if basic authentication or a token is used.  |
| Protect the webhook secret | Use webhook secrets that are _unique per customer_. Also consider rotating / changing the secret periodically. If you do implement a secret rotation, do note that you need to accept payloads signed with both the old and the new secret for up to 5 minutes after the change. |
| Secure the webhook and JWT action transport | Both the webhook and action URLs must be HTTPS with a valid certificate signed by a trusted Certificate Authority. Self-signed certificates are not supported. |
| Minimize required xAPI access | Try to minimize the xAPI access required in your manifest. It's tempting to use wildcards to avoid having to specify individual statuses or commands, but this makes it a lot harder for the admin to know and understand what the integration is actually allowed to do. |
| Securely store data | All data received by the integration should be securely stored and encrypted at rest. This holds especially true for the `clientId`, `clientSecret` and `refreshToken`. |
