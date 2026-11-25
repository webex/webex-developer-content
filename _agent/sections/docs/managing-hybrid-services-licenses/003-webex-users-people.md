---
type: Excerpt
canonical_url: https://developer.webex.com/docs/managing-hybrid-services-licenses
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Webex Users (People)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/managing-hybrid-services-licenses). [Full Markdown](../../../../docs/managing-hybrid-services-licenses.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex API includes several methods which can be used by administrators to programmatically manage license usage of Webex Hybrid Services.

## Selected section

## Webex Users (People)

Webex administrators (both full and read-only administrators) can view all people either in bulk or individually. Using the [People Resource](https://developer.webex.com/docs/api/v1/people) of the API, full administrators can add and remove licenses from individual users.

Licenses can be applied either when people are created or via an update to individual existing people.

### Listing All Users

Full administrators for the organization can [list all people within an organization](https://developer.webex.com/docs/api/v1/people/list-people) to see licenses associated with each person. Query parameters allow filtering by email or name—these options are not required for administrators.

#### Example

`GET https://webexapis.com/v1/people`

```json
{
  "items" : [ {
    "id" : "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY",
    "emails" : [ "john.andersen@foo.com" ],
    "displayName" : "John Andersen",
    "orgId" : "OTZhYmMyYWEtM2RjYy0xMWU1LWExNTItZmUzNDgxOWNkYzlh",
    "licenses" : [
      "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMTIzNDU2NzgtOTBhYi1jZGVmLTEyMzQtNTY3ODkwYWJjZGVmOkFBXzEyMzQ1Njc4LTkwYWItY2RlZi0xMjM0LTU2Nzg5MGFiY2RlZg",
      "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMDEyMzQ1NjctODkwYS1iY2RlLWYwMTItMzQ1Njc4OTBhYmNkOkFBXzAxMjM0NTY3LTg5MGEtYmNkZS1mMDEyLTM0NTY3ODkwYWJjZA"
    ]
    ... extra response data omitted ...
  } ]
}
```

### Listing Individual Users

To see which licenses are associated with individual users, use their person ID to [retrieve their details](https://developer.webex.com/docs/api/v1/people/get-person-details), which will include the licenses associated with their account.

#### Example

`GET https://webexapis.com/v1/people/Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY`

```json
{
  "id" : "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY",
  "emails" : [ "john.andersen@foo.com" ],
  "displayName" : "John Andersen",
  "orgId" : "OTZhYmMyYWEtM2RjYy0xMWU1LWExNTItZmUzNDgxOWNkYzlh",
  "licenses" : [
    "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMTIzNDU2NzgtOTBhYi1jZGVmLTEyMzQtNTY3ODkwYWJjZGVmOkFBXzEyMzQ1Njc4LTkwYWItY2RlZi0xMjM0LTU2Nzg5MGFiY2RlZg",
    "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMDEyMzQ1NjctODkwYS1iY2RlLWYwMTItMzQ1Njc4OTBhYmNkOkFBXzAxMjM0NTY3LTg5MGEtYmNkZS1mMDEyLTM0NTY3ODkwYWJjZA"
  ]
  ... extra response data omitted ...
}
```

This user has both Messaging (`Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMTIzNDU2NzgtOTBhYi1jZGVmLTEyMzQtNTY3ODkwYWJjZGVmOkFBXzEyMzQ1Njc4LTkwYWItY2RlZi0xMjM0LTU2Nzg5MGFiY2RlZg`) and the Hybrid Call Aware licenses (`Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMDEyMzQ1NjctODkwYS1iY2RlLWYwMTItMzQ1Njc4OTBhYmNkOkFBXzAxMjM0NTY3LTg5MGEtYmNkZS1mMDEyLTM0NTY3ODkwYWJjZA`) enabled.

### Creating Webex Users

When creating Webex users, licenses which will be enabled for the new user can be included in the request. Include specific Hybrid Services licenses to enable those services for the new user. Be sure to use the license IDs retrieved from `/licenses` as described earlier in this document—license IDs will be different from the examples here and between different organizations. See the [Create a Person reference](https://developer.webex.com/docs/api/v1/people/create-a-person) for more details about how to create people.

#### Example

`POST https://webexapis.com/v1/people`

Example Request Body

```json
{
  "emails" : [ "john.andersen@foo.com" ],
  "displayName" : "John Andersen",
  "firstName" : "John",
  "lastName" : "Andersen",
  "avatar" : "URL",
  "orgId" : "OTZhYmMyYWEtM2RjYy0xMWU1LWExNTItZmUzNDgxOWNkYzlh",
  "roles" : [ "RoleID1", "RoleID2" ],
  "licenses" : [
    "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMTIzNDU2NzgtOTBhYi1jZGVmLTEyMzQtNTY3ODkwYWJjZGVmOkFBXzEyMzQ1Njc4LTkwYWItY2RlZi0xMjM0LTU2Nzg5MGFiY2RlZg",
    "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMDEyMzQ1NjctODkwYS1iY2RlLWYwMTItMzQ1Njc4OTBhYmNkOkFBXzAxMjM0NTY3LTg5MGEtYmNkZS1mMDEyLTM0NTY3ODkwYWJjZA"
    ]
}
```

This user will be granted Messaging and Hybrid Call Aware licenses.

Example Response

```json
{
  "id" : "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY"
  "emails" : [ "john.andersen@foo.com" ],
  "displayName" : "John Andersen",
  "firstName" : "John",
  "lastName" : "Andersen",
  "avatar" : "URL",
  "orgId" : "OTZhYmMyYWEtM2RjYy0xMWU1LWExNTItZmUzNDgxOWNkYzlh",
  "roles" : [ "RoleID1", "RoleID2" ],
  "licenses" : [
    "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMTIzNDU2NzgtOTBhYi1jZGVmLTEyMzQtNTY3ODkwYWJjZGVmOkFBXzEyMzQ1Njc4LTkwYWItY2RlZi0xMjM0LTU2Nzg5MGFiY2RlZg",
    "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMDEyMzQ1NjctODkwYS1iY2RlLWYwMTItMzQ1Njc4OTBhYmNkOkFBXzAxMjM0NTY3LTg5MGEtYmNkZS1mMDEyLTM0NTY3ODkwYWJjZA"
    ]
  "created" : "2015-10-18T14:26:16+00:00",
  "timezone" : "America/Denver",
  "lastActivity" : "2015-10-18T14:26:16+00:00",
}
```

### Updating Webex Users

To add to or remove licenses from an existing person, update their record with the new license IDs. Include all attributes for the person (as described in the [Update People reference](https://developer.webex.com/docs/api/v1/people/update-a-person)), specifically including only the licenses which should be enabled for the person.

If the person is currently assigned a license which is not included in the update request it will be unassigned from that person. Be sure to include all other details for the person, as the `PUT` operation expects all user details to be present in the request. It is common to first `GET` the person details, make changes, and then `PUT` those changes to ensure the other information is accurate.

Use the license IDs retrieved from `/licenses` as described earlier—license IDs will be different from the examples here and between different organizations.

#### Example

`PUT https://webexapis.com/v1/people/Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY`

Example Request Body

```json
{
  "emails" : [ "john.andersen@foo.com" ],
  "displayName" : "John Andersen",
  "firstName" : "John",
  "lastName" : "Andersen",
  "avatar" : "URL",
  "orgId" : "OTZhYmMyYWEtM2RjYy0xMWU1LWExNTItZmUzNDgxOWNkYzlh",
  "roles" : [ "RoleID1", "RoleID2" ],
  "licenses" : [
    "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMTIzNDU2NzgtOTBhYi1jZGVmLTEyMzQtNTY3ODkwYWJjZGVmOkFBXzEyMzQ1Njc4LTkwYWItY2RlZi0xMjM0LTU2Nzg5MGFiY2RlZg",
    "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMDEyMzQ1NjctODkwYS1iY2RlLWYwMTItMzQ1Njc4OTBhYmNkOkFBXzAxMjM0NTY3LTg5MGEtYmNkZS1mMDEyLTM0NTY3ODkwYWJjZA"
    ]
}
```

Example Response

```json
{
  "id" : "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY"
  "emails" : [ "john.andersen@foo.com" ],
  "displayName" : "John Andersen",
  "firstName" : "John",
  "lastName" : "Andersen",
  "avatar" : "URL",
  "orgId" : "OTZhYmMyYWEtM2RjYy0xMWU1LWExNTItZmUzNDgxOWNkYzlh",
  "roles" : [ "RoleID1", "RoleID2" ],
  "licenses" : [
    "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMTIzNDU2NzgtOTBhYi1jZGVmLTEyMzQtNTY3ODkwYWJjZGVmOkFBXzEyMzQ1Njc4LTkwYWItY2RlZi0xMjM0LTU2Nzg5MGFiY2RlZg",
    "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMDEyMzQ1NjctODkwYS1iY2RlLWYwMTItMzQ1Njc4OTBhYmNkOkFBXzAxMjM0NTY3LTg5MGEtYmNkZS1mMDEyLTM0NTY3ODkwYWJjZA"
    ]
  "created" : "2015-10-18T14:26:16+00:00",
  "timezone" : "America/Denver",
  "lastActivity" : "2015-10-18T14:26:16+00:00",
}
```
