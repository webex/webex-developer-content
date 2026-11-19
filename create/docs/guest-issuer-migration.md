---
type: Guide
title: Guest Issuer Migration Guide
display_title: Guest Issuer Migration Guide
canonical_url: https://developer.webex.com/docs/guest-issuer-migration
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/guest-issuer-migration)

Migrate an existing legacy Guest Issuer application to [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) by binding your guest issuer to a Service App before you issue guest tokens.

## Overview

This page is for **migrating** from a legacy Guest Issuer application. If you are building a **new** guest integration with no legacy Guest Issuer, use [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management)—you do not need to call `bindGuestIssuer`.

Guest Issuer applications used a shared JWT secret to create guest tokens. Service Apps use the [Guest Management API](https://developer.webex.com/admin/docs/api/v1/guest-management) instead. For organizations with an existing Guest Issuer, a one-time **bind** links that issuer to your Service App so guest tokens continue to use the same guest issuer organization.

Binding is a **one-time setup** performed by a Webex organization administrator. Your application does not call the bind API at runtime. After a successful bind, issue guest tokens with `POST /v1/guests/token` using your Service App access token—the same runtime flow described on [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management).

## Before You Begin

Complete all of the following before binding. Skipping a step is a common cause of `403` or `409` errors.

### Prerequisites

- A legacy Guest Issuer application that already exists for your organization.
- A Service App created with at least `guest-issuer:write` and `guest-issuer:read` scopes. See [Using Webex Service Apps](https://developer.webex.com/docs/service-apps).
- A Webex organization **Full Admin** to authorize the Service App and perform the bind.
- The personal access token of the **developer who created the legacy Guest Issuer** (with `spark:applications_read`) to list issuers—see [List Your Guest Issuers](#list-your-guest-issuers) below.

On the migration path, do **not** call `POST /v1/guests/token` with the Service App until **after** `bindGuestIssuer` returns `204 No Content`. If you call `POST /v1/guests/token` before binding, the request can still return `200 OK`, but developer-applications may auto-create a **new** guest issuer for the Service App machine account instead of using your legacy issuer. That Service App can no longer be used for a clean migration to the legacy issuer.

**How to recognize this state before you bind:**

- `POST /v1/guests/token` returned `200 OK` before `bindGuestIssuer` returned `204 No Content`.
- `GET /v1/guests/count` returns a value greater than `0` before binding completes.

`bindGuestIssuer` may still return `204 No Content` even after a premature guest token call, so a successful bind does **not** mean the migration is clean. If you see either signal above, create a new Service App, authorize it, bind the legacy issuer, and only then call `POST /v1/guests/token`.

## List Your Guest Issuers

If you already created guest issuers, list them and read each item's `id`. Use that value as `guestIssuerId` when you bind.

Use the developer who originally created the legacy Guest Issuer application—the same developer account that had access when Guest Issuer apps were managed in the developer portal. That developer's personal access token must include the `spark:applications_read` scope.

### Request

```bash
curl --request GET \
  --header "Authorization: Bearer PERSONAL_ACCESS_TOKEN" \
  https://webexapis.com/v1/jwt
```

### Response

The response includes an `items` array. Each item includes `id`, `name`, and `created`. Secrets are **not** returned on the list. Pick the `id` of the issuer you want to bind and pass it as `guestIssuerId` in the bind request.

```json
{
  "items": [
    {
      "id": "Y2lzY29zcGFyazovL3VybjpURUFNOnVzLWVhc3QtMV9pbnQxMy9PUkcvZGVmNTY3ODk=",
      "name": "My Guest Issuer",
      "created": "2024-01-15T10:00:00.000Z"
    }
  ]
}
```

If `items` is empty, confirm you are using the original Guest Issuer creator's token with `spark:applications_read`. If you are starting a **new** integration without a legacy issuer, you do not need this step—see [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) instead.

## Authorize Your Service App

Before you bind, a Webex organization **Full Admin** must authorize the Service App for your organization in Control Hub.

1. In the [developer portal](https://developer.webex.com), the Service App developer clicks **Request Admin Authorization** on the Service App details page so the app appears in the organization's Control Hub. If you are a Full Admin in your own org, you can skip this step and authorize the app directly.
2. The Full Admin logs in to [Control Hub](https://admin.webex.com), opens **Management** > **Apps** > **Service Apps**, selects the Service App, and reviews its description and requested scopes.
3. The admin clicks **Authorize**, then **Save**.

If the Service App does not appear in Control Hub, ask the developer to submit it for admin authorization first. For Service App creation, scopes, and the full developer and admin flows, see [Using Webex Service Apps](https://developer.webex.com/docs/service-apps).

## Bind a Guest Issuer

An org admin binds the legacy guest issuer to the authorized Service App. This is a **migration-only**, one-time call.

```bash
curl --request POST \
  --header "Authorization: Bearer ORG_ADMIN_ACCESS_TOKEN" \
  --header "Content-Type: application/json" \
  --data '{"guestIssuerId": "GUEST_ISSUER_ID_FROM_LIST"}' \
  https://webexapis.com/v1/applications/SERVICE_APP_ID/bindGuestIssuer
```

| Item               | Detail                                                             |
| ------------------ | ------------------------------------------------------------------ |
| **Method**         | `POST`                                                             |
| **Endpoint**       | `/v1/applications/{applicationId}/bindGuestIssuer`                 |
| **Caller**         | Webex organization administrator (human user)                      |
| **Token**          | Org admin OAuth access token with `spark-admin:applications_write` |
| **Path parameter** | `applicationId` — your Service App ID (`SERVICE_APP_ID`)           |
| **Request body**   | `guestIssuerId` — the `id` from `GET /v1/jwt`                      |
| **Success**        | `204 No Content` (empty body)                                      |

The Service App machine account token, bot tokens, and personal developer tokens (without org admin role) are **not** valid for this call.

## Migration Workflow

| Step | Actor       | Action                                                                              | Token                                             | Success signal               |
| ---- | ----------- | ----------------------------------------------------------------------------------- | ------------------------------------------------- | ---------------------------- |
| 1    | Developer   | List guest issuers: `GET /v1/jwt`                                                   | Personal access token (`spark:applications_read`) | `items[]` with target `id`   |
| 2    | Developer   | Create Service App with `guest-issuer:read` and `guest-issuer:write`                | —                                                 | Service App in My Webex Apps |
| 3    | Org admin   | Authorize Service App in Control Hub (**Management** > **Apps** > **Service Apps**) | —                                                 | Service App authorized       |
| 4    | Org admin   | `POST /v1/applications/{id}/bindGuestIssuer`                                        | Org admin OAuth token                             | `204 No Content`             |
| 5    | Developer   | Obtain Service App access token                                                     | Service App credentials                           | Access token issued          |
| 6    | Service App | `POST /v1/guests/token`                                                             | Service App access token                          | Guest access token returned  |

Do not perform step 6 until step 4 succeeds.

## After Migration

After `bindGuestIssuer` succeeds, update your legacy integration to stop generating shared-secret JWTs and instead issue guest tokens through `POST /v1/guests/token` using the Service App access token, as documented in [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management).



> **Do not use the legacy JWT flow after bind**
>
> After `bindGuestIssuer` succeeds, the legacy shared secret for that guest issuer is disabled. Do not continue using the legacy JWT login flow for that issuer. From that point forward, issue guest tokens only with `POST /v1/guests/token` using the Service App access token.



Guest users and history associated with the bound issuer organization are preserved through the migration when you complete the bind **before** issuing any Service App guest tokens.

## Troubleshooting

Errors use the standard Webex API error format with `message` and `trackingId` fields.

| HTTP status          | Typical cause                                                             | What to do                                                                                                                                                                                      |
| -------------------- | ------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `400 Bad Request`    | Missing or invalid `guestIssuerId`                                        | Send the `id` from `GET /v1/jwt` in the request body                                                                                                                                            |
| `400 Bad Request`    | Target is not a Service App                                               | Verify `applicationId` refers to a Service App                                                                                                                                                  |
| `403 Forbidden`      | Guest Issuer migration is not enabled                                     | Contact [Webex support](https://developer.webex.com/support) or your account team                                                                                                                                          |
| `403 Forbidden`      | Service App missing `guest-issuer:write`                                  | Recreate or update the Service App scopes                                                                                                                                                       |
| `403 Forbidden`      | Guest issuer not eligible for this org                                    | Use an issuer created by your organization                                                                                                                                                      |
| `403 Forbidden`      | Caller is not an org admin or app not authorized                          | Authorize the app with a Full Admin token first                                                                                                                                                 |
| `404 Not Found`      | Issuer does not exist                                                     | Re-check `guestIssuerId` from the list response                                                                                                                                                 |
| `409 Conflict`       | Binding already exists                                                    | Do not call bind again; contact support if the wrong app is bound                                                                                                                               |
| `200 OK` (premature) | `POST /v1/guests/token` succeeded before `bindGuestIssuer` returned `204` | The Service App may have auto-created its own guest issuer. Check `GET /v1/guests/count`; if it is greater than `0` before binding, create a **new** Service App, authorize, bind, then migrate |
| —                    | Guest token `id` does not match legacy guest users after bind             | You likely issued Service App guest tokens before binding. Create a **new** Service App, authorize, bind first, then re-issue tokens for migrated subjects                                      |

## De-authorization and Re-authorization

`bindGuestIssuer` is a **one-time** setup step. If an org admin removes and later restores Service App authorization, the guest issuer binding **remains**.

- **Do not** call `bindGuestIssuer` again after re-authorization—a second bind returns `409 Conflict`.
- After re-authorization, exchange Service App credentials for a **new** access token, then continue using `POST /v1/guests/token`.
- Guest users and the guest issuer organization are unchanged across de-authorization and re-authorization.

A guest issuer binding **cannot be transferred** to a different Service App through the public API. If you must use a different Service App with the same guest issuer, contact [Webex support](https://developer.webex.com/support).

## FAQ

### Is bind the same API I use to get guest tokens?

No. `bindGuestIssuer` is a one-time admin setup call. Guest tokens are issued at runtime via `POST /v1/guests/token` using the Service App access token.

### Can I bind multiple guest issuers to one Service App?

For a given authorized organization, no. A Service App can have only one bound guest issuer per authorized org. Each guest issuer can only be bound once. If the same Service App is authorized by multiple orgs, each org can have its own eligible guest issuer binding.

### Can I unbind or change the guest issuer?

No public API removes or changes an existing binding. Contact [Webex support](https://developer.webex.com/support) for guidance.

### Do I need to call bind again after re-authorizing the Service App?

No. Obtain a new Service App access token and continue using `POST /v1/guests/token`.

### What if I already called `/guests/token` before binding?

There is no API to reset a Service App that already issued guest tokens before binding. A premature `POST /v1/guests/token` can return `200 OK` and auto-create a Service App-owned guest issuer, which is separate from your legacy issuer.

Check whether `GET /v1/guests/count` is greater than `0` before `bindGuestIssuer` completes. If so, or if guest token `id` values do not match your legacy guest users after binding, create a new Service App, have an org admin authorize and bind **before** any guest token calls, and migrate your integration to the new app.

## Related Documentation

- [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) — greenfield setup and runtime guest tokens
- [Guest Issuer](https://developer.webex.com/docs/guest-issuer) — legacy Guest Issuer reference (deprecated)
- [Using Webex Service Apps](https://developer.webex.com/docs/service-apps) — create, approve, and authorize Service Apps
- [Guest Management API reference](https://developer.webex.com/admin/docs/api/v1/guest-management) — `POST /v1/guests/token` and related endpoints
