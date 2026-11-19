---
type: Guide
title: Troubleshoot Webex Connect APIs
display_title: Troubleshooting APIs
canonical_url: https://developer.webex.com/docs/webex-connect-troubleshooting-apis
content_type: documentation
product_group:
- webex-connect
categories:
- webex-connect
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-connect-troubleshooting-apis)

Use this checklist to diagnose common failures when calling Webex Connect APIs.

## Start by isolating the problem

1. Reproduce the issue with the smallest valid request in **Try Out** on the exact API Reference operation.
2. Compare the method, path, endpoint, headers, query parameters, and request body with the operation definition.
3. Record the HTTP status, response body, `transid`, optional `trackingid`, and timestamp.
4. Confirm that the user can access the organization and has permission to perform the requested operation.

## The API returns 401

- Confirm that the request includes the authentication credentials required by the API.
- If the API uses a bearer token, obtain a current token if it has expired.
- Ensure that credentials are complete, correctly formatted, and sent in the required header.

## The API returns 403

- Confirm that the token includes the scope required by the operation.
- If the API requires an organization identifier, confirm that it identifies an organization the user can access.
- Confirm that the user has permission to perform the requested operation.

## The API returns 400

- Validate the JSON syntax and `Content-Type` header.
- Check that all required query parameters and headers are present and use allowed values.
- Verify identifier formats and required request body fields.
- Check API-specific configuration objects against the operation definition.

## The endpoint cannot be reached

- Use the API base URL documented for the API family.
- Confirm that the selected endpoint corresponds to the organization's region.
- Confirm that the network permits outbound HTTPS access to the API hostname.

## The request is limited

- Reduce the request rate and review the limits documented for the API family and operation.
- Avoid concurrent updates to the same resource.
- Before repeating a create or update request, verify whether the earlier request succeeded.

## Contact support

Provide a sanitized request and response, the operation and HTTP method, timestamp with time zone, organization region, HTTP status, `transid`, and any `trackingid` you supplied. Include the expected and actual behavior.

Never include access tokens, credentials, client secrets, or other sensitive configuration data.
