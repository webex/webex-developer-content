---
type: Guide
title: Webex Connect API Rate Limits
display_title: Rate Limits
canonical_url: https://developer.webex.com/docs/webex-connect-rate-limits
content_type: documentation
product_group:
- webex-connect
categories:
- webex-connect
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-connect-rate-limits)

Webex Connect applies rate limits across its API families to protect service availability and provide predictable performance. The applicable limit depends on the API family, operation, and limits configured for your organization.

## Configuration APIs

Configuration APIs use limits defined for each API family and operation. These limits are evaluated independently of Messaging API throughput.

### Digital Channel Onboarding APIs

Rate limits apply to operations that create, retrieve, or update digital channel assets. The API Reference is authoritative for the limit that applies to each operation, including its evaluation scope and time window.

## When a limit is exceeded

Reduce the request rate and follow the rate-limit handling documented for the API family.

Do not retry rate-limited Digital Channel Onboarding API requests. Verify the current state of the asset before performing any further operation.

## Best practices

- Cache stable resource information instead of retrieving it before every dependent action.
- Avoid sending concurrent updates for the same resource.
- Stagger bulk jobs instead of sending every request at the same time.
- Record the operation, timestamp, organization ID, HTTP status, and transaction identifier for repeated limit responses.
