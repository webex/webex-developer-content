---
type: Guide
title: Access the Webex Connect API
display_title: Access the API
canonical_url: https://developer.webex.com/docs/webex-connect-access-the-api
content_type: documentation
product_group:
- webex-connect
categories:
- webex-connect
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-connect-access-the-api)

Use a Webex personal access token to call the digital asset onboarding APIs for Email, Live Chat, and In-App assets.

## Before you begin

Confirm that:

- your Webex Connect organization is active;
- your user has permission to manage the required digital assets;
- the personal access token includes the scope required by the asset operation;
- you know the organization ID to send in `x-organization-id`; and
- you are using the base URL and API version shown in the API Reference.

## Authenticate the request

Send the personal access token using the bearer scheme:

```http
Authorization: Bearer <personal-access-token>
```

Personal access tokens are the supported authentication method for these digital asset APIs.

## Provide the organization and request details

Include the organization ID and JSON media type where the operation requires them:

```http
x-organization-id: <organization-id>
Content-Type: application/json
```

You can also provide a unique `trackingid` header to help correlate the request during troubleshooting.

Use the exact HTTP method, path, query parameters, and request body defined for the asset operation. For example, Email asset creation uses `POST /v2/digital/app` with `channel=email`.

## Try an operation in the Developer Portal

1. Open the required asset operation under **API Reference**.
2. Select **Use personal access token**.
3. Enter the organization ID and all required parameters and fields.
4. Review the generated request and select **Run**.
5. Record the HTTP status and the `transid` returned in the response.

## Handle the response

A successful response confirms that the requested asset operation completed. Validate the returned asset details before storing the result. For a failed request, use the HTTP status, response `code`, `description`, and `transid` to identify the cause.

## Next steps

- [Personal Access Token](https://developer.webex.com/webex-connect/docs/webex-connect-personal-access-token)
- [Create Your First Digital Asset](https://developer.webex.com/webex-connect/docs/webex-connect-create-your-first-digital-asset)
