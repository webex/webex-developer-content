---
type: Article
title: Prepare for Upcoming Webex Contact Center API Domain Discovery Changes
canonical_url: https://developer.webex.com/blog/discover-the-right-api-domain-for-webex-contact-center
content_type: blog
date: '2026-10-15'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/discover-the-right-api-domain-for-webex-contact-center)

**Upcoming change — availability planned by January 15, 2027.** Webex Contact Center is preparing changes to how applications discover the API domain for their organization. This post previews the expected integration changes and explains how developers and partners can prepare. The planned date describes availability; any required migration deadline will be stated separately.

Domain discovery will give applications a common starting point for Webex Contact Center (WxCC) API integrations. An application will retrieve the domain for its organization and use it to build API requests without maintaining its own regional URL mapping.

Discovery will tell an application which domain to use when traffic moves during failover or failback for regional disaster recovery. A hardcoded regional URL could keep sending requests to an outdated access path.

### How the discovery flow will work

When the changes become available, applications will query the Webex Contact Center global discovery endpoint before calling WxCC APIs. They will use the returned domain as the base for requests, combined with the documented path for each API.

Replacing configured regional domains and direct backend URLs with this discovery flow is the expected integration update.

### Plan for cache refresh and connection renewal

The planned flow includes two client behaviors beyond the first discovery request:

- **Cache the discovered domain.** For continuous API use, keep it for at least 15 minutes and no more than 30 minutes. Reuse it between refreshes rather than calling discovery for every request.
- **Close stale connections.** When an API response indicates failure (a non-2xx status code) and includes the `X-WXCC-Connection: close` header, close the connection and establish a new one before sending further requests.

Refresh discovery when the cache interval expires or recovery requires it. A stale connection still needs replacing even if the returned domain has not changed.

### What you can do now

Identify where your application selects its WxCC API base domain. Inventory hardcoded regional domains and direct backend URLs, and review where your application manages cached domains and persistent connections. Use this inventory to plan and estimate the integration update.

### What to do when the changes become available

Follow the published API documentation to implement domain discovery, then validate domain refresh and connection renewal in your test environment.

For help planning your integration update, contact [Webex Developer Support](https://developer.webex.com/support).
