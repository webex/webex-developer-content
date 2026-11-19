---
type: Guide
title: Webex Connect API Status and Error Codes
display_title: Status and Error Codes
canonical_url: https://developer.webex.com/docs/webex-connect-status-and-error-codes
content_type: documentation
product_group:
- webex-connect
categories:
- webex-connect
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-connect-status-and-error-codes)

Webex Connect APIs use HTTP status codes and response bodies to communicate the outcome of a request.

## HTTP status codes

| Status | Meaning |
|---|---|
| `200 OK` | The request was completed successfully. |
| `400 Bad Request` | A required query parameter, header, or body field is missing or invalid. |
| `401 Unauthorized` | The bearer token is missing, invalid, or expired. |
| `403 Forbidden` | The user does not have access to the organization or permission to perform the requested operation. |
| `500 Internal Server Error` | Webex Connect could not complete the operation because of an internal error. |

The API Reference for each operation is authoritative for the response codes and schemas it supports.

## Response fields

API responses can include these common fields:

| Field | Description |
|---|---|
| `code` | API result or error code. |
| `description` | Human-readable result or error description. |
| `transid` | Transaction identifier used to trace the request. |

Additional response fields vary by API and operation. See the API Reference for the response schema supported by each operation.

## Authentication and authorization errors

For `401 Unauthorized`, verify that the request includes the authentication credentials required by the API and that they are valid and current. For APIs that use bearer-token authentication, verify this header:

```http
Authorization: Bearer <access-token>
```

For `403 Forbidden`, verify the required scope, the user's organization access, and permission to perform the requested operation. A valid token alone is not sufficient.

## Validation errors

For `400 Bad Request`, check the operation definition for:

- required query parameters and headers;
- valid identifiers and values;
- required request body fields; and
- API-specific configuration objects.

## Troubleshooting data

Record the HTTP status, `code`, `description`, `transid`, timestamp, operation, and organization ID. If you supplied a `trackingid` request header, record that value too. Never log or share personal access tokens, client secrets, credentials, or other sensitive configuration data.
