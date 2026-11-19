---
type: Guide
title: Webex Connect API Endpoints and Regions
display_title: API Endpoints and Regions
canonical_url: https://developer.webex.com/docs/webex-connect-api-endpoints-and-regions
content_type: documentation
product_group:
- webex-connect
categories:
- webex-connect
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-connect-api-endpoints-and-regions)

Use the API base URL associated with the API family and the region in which your organization is hosted.

## Select the correct endpoint

The Webex Developer Portal is globally available, but your organization and its assets are hosted regionally. The operation in the API Reference displays the base URL and version supported for the selected environment.

### Digital Channel Onboarding APIs

For Digital Channel Onboarding APIs, use the following base URL for the region in which your organization is hosted:

| Region | Environment | Digital Channel Onboarding API base URL |
| --- | --- | --- |
| Ireland | `prodeu2` | `https://assetmanagement.eu.webexconnect.io/connectapi` |
| Oregon | `produs1` | `https://assetmanagement.us.webexconnect.io/connectapi` |
| London | `prodeu1` | `https://assetmanagement.uk.webexconnect.io/connectapi` |
| Canada | `prodca1` | `https://assetmanagement.ca.webexconnect.io/connectapi` |
| Sydney | `prodanz1` | `https://assetmanagement.au.webexconnect.io/connectapi` |
| Singapore | `prodsg1` | `https://assetmanagement.sg.webexconnect.io/connectapi` |
| India | `prodind1` | `https://assetmanagement.in.webexconnect.io/connectapi` |
| Japan | `prodjp1` | `https://assetmanagement.au.webexconnect.io/connectapi` |

The Sydney and Japan environments currently use the same Digital Channel Onboarding API base URL.

Do not construct a Digital Channel Onboarding API hostname by copying the hostname used by another Webex Connect API family. Use the complete base URL shown for the Digital Channel Onboarding operation and keep it configurable in your application.

## Build a request URL

Combine the base URL shown in the API Reference with the operation path. For example, the Email create operation uses this path:

```text
<digital-channel-onboarding-api-base-url>/v2/digital/app?channel=email
```

Use HTTPS and preserve the host, API version, path, and channel value exactly as documented.

## Organization routing

Digital Channel Onboarding requests require the organization identifier in the `x-organization-id` header:

```http
x-organization-id: <organization-id>
```



## Next steps

- [Access the API](https://developer.webex.com/docs/webex-connect-access-the-api)
- [Authentication](https://developer.webex.com/docs/webex-connect-authentication)
