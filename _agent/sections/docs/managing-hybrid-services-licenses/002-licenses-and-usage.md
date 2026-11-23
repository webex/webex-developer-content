---
type: Excerpt
canonical_url: https://developer.webex.com/docs/managing-hybrid-services-licenses
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Licenses and Usage
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/managing-hybrid-services-licenses). [Full Markdown](../../../../docs/managing-hybrid-services-licenses.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex API includes several methods which can be used by administrators to programmatically manage license usage of Webex Hybrid Services.

## Selected section

## Licenses and Usage

All Webex licenses for an organization can be retrieved via the `/licenses` endpoint of the API. This will include Hybrid Services licenses if they are enabled for the particular organization.

Hybrid Services licenses will always be displayed with a total unit quantity of `1` and a consumed unit value of `0`. As licenses are assigned to users, these values will not change.

### Listing Licenses

License information can be retrieved for any organization where the calling user is granted access. If no organization ID is specified in the request, the calling user’s organization will be used. Information about each license associated with the organization will be returned. See the [List Licenses reference](https://developer.webex.com/docs/api/v1/licenses/list-licenses) for more details.

#### Example

`GET https://webexapis.com/v1/licenses`

```json
{
  "items" : [ {
    "id" : "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMTIzNDU2NzgtOTBhYi1jZGVmLTEyMzQtNTY3ODkwYWJjZGVmOkFBXzEyMzQ1Njc4LTkwYWItY2RlZi0xMjM0LTU2Nzg5MGFiY2RlZg",
    "name" : "Messaging",
    "totalUnits" : "100",
    "consumedUnits" : "17"
  }, {
    "id" : "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMDEyMzQ1NjctODkwYS1iY2RlLWYwMTItMzQ1Njc4OTBhYmNkOkFBXzAxMjM0NTY3LTg5MGEtYmNkZS1mMDEyLTM0NTY3ODkwYWJjZA",
    "name" : "Hybrid Call Aware",
    "totalUnits" : "1",
    "consumedUnits" : "0"
  } ]
}
```

### License Combinations and Dependencies

#### Google and Exchange Calendars

Organizations may have both Hybrid Exchange Calendar and Hybrid Google Calendar licenses enabled at the organization-level. Individual users may not have both of these services enabled at the same time. Attempting to add both licenses to the same user (to enable both services for that user) will result in an API error: `Cannot enable both exchange and google calendar service for the same user.`

#### Hybrid Call Aware and Hybrid Call Connect

The Hybrid Call Connect license cannot be added to users unless they also have the Hybrid Call Aware license enabled. Attempting to add Hybrid Call Connect to a user without Hybrid Call Aware will result in an API error: `Cannot enable call connect service without call aware service.`
