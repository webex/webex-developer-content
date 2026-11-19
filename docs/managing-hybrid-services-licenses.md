---
type: Guide
title: Managing Hybrid Services Licenses | Consolidated Guide
display_title: Hybrid Services
canonical_url: https://developer.webex.com/docs/managing-hybrid-services-licenses
content_type: documentation
product_group:
- webex-suite
categories:
- admin
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/managing-hybrid-services-licenses)

The Webex API includes several methods which can be used by administrators to programmatically manage license usage of Webex Hybrid Services.

## Overview

The following Hybrid Services licenses can be managed via the Webex API:

- Hybrid Call Aware
- Hybrid Call Connect
- Hybrid Exchange Calendar
- Hybrid Google Calendar

### Requirements

- API users must be assigned the “Full Administrator” role for their organization to access license information and display information about all people within the organization.
- API users must be assigned the “Full Administrator” role or have the `spark-admin:people_write` scope enabled to add licenses to users.

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

## Webex Resource Groups

Resource Groups are collections of on-premise clusters which provide Hybrid Services to a subset of people in an organization. Your organization should have Hybrid Services enabled before using Resource Groups. When a Webex user is assigned a Hybrid Services license, they will be automatically associated to an on-premise cluster for that service. Resource Groups may be used to define a subset of users and clusters for a specific purpose, such as data regulation or class of service. For more information about when to use Resource Groups, see [Resource Groups for Webex Hybrid Services](https://help.webex.com/kkibf0/).

### Resource Groups API

Resource Groups are created and managed in [Webex Control Hub](https://admin.webex.com). The [Resource Groups API](https://developer.webex.com/docs/api/v1/resource-groups) can be used to retrieve information about Resource Groups for an organization. Listing all groups or viewing details for a particular group requires an administrator auth token with the `spark-admin:resource_groups_read` scope.

### Resource Group Memberships API

Resource Group Memberships represent a user's assignment to a Resource Group for a particular Hybrid Service. When Hybrid Services licenses are associated with users, they are assigned to a “default” Resource Group for the service. The [Resource Group Memberships API](https://developer.webex.com/docs/api/v1/resource-group-memberships) can be used to retrieve information about current Resource Group assignments and to change the Resource Group for a user's specific Hybrid Service.

All users with Hybrid Services licenses will be associated with a Resource Group for each service, either the default group or a specific one. Since users always belong to a Resource Group for each service, Resource Group Memberships cannot be created or deleted via the Webex API. Instead, users may remain associated with the default group for the service, or be associated with specific Resource Groups. The [Update a Resource Group Membership](https://developer.webex.com/docs/api/v1/resource-group-memberships/update-a-resource-group-membership) endpoint can be used to move users between groups. To disassociate a user with a particular Resource Group, they should be moved back to the default group.

Viewing Resource Group Memberships requires an administrator auth token with the `spark-admin:resource_group_memberships_read` scope. Updating memberships requires an administrator auth token with the `spark-admin:resource_group_memberships_write` scope.

### Resource Group API Usage Example

For example, to get started with managing Resource Groups via the Webex API, an Organization Administrator would generally go through the following steps:

#### 1. Create a Resource Group

Create a Resource Group for a Hybrid Service in [Webex Control Hub](https://admin.webex.com).

#### 2. Assign Licenses to a User

Use the [Licenses API](https://developer.webex.com/docs/api/v1/licenses) to retrieve all licenses for your organization. Then, determine which Hybrid Services license you wish to apply. Apply this license to a user, along with any current licenses the user may be associated with.

*See "Updating Webex Users" above for an example.*

#### 3. Find the Resource Group ID

Use the [Resource Groups API](https://developer.webex.com/docs/api/v1/resource-groups) to find the ID of the new Resource Group. Make note of this `id`. You'll use this to change the user's Resource Group for this Hybrid Service.

`GET https://webexapis.com/v1/resourceGroups`

```json
{
  "items" : [ {
    "id" : "Y2lzY29zcGFyazovL3VzL1JFU09VUkNFX0dST1VQLzFjY2JiYzE3LWQ2MTYtNGQ3NC04NjRiLWIxZjNiMDcwMWZiYQ",
    "name" : "Resource Group 1",
    "orgId" : "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi85NmFiYzJhYS0zZGNjLTExZTUtYTE1Mi1mZTM0ODE5Y2RjOWE"
  } ]
}
```

#### 4. Find the User's Current Resource Group Membership

Use the [List Resource Group Memberships endpoint](https://developer.webex.com/docs/api/v1/resource-group-memberships/list-resource-group-memberships) with a `licenseId` for a Hybrid Service and the user's `personId` to find the current Resource Group Membership. If the user is not associated with a Resource Group,  this membership will represent the default Resource Group. Make note of the `id`.

`GET https://webexapis.com/v1/resourceGroup/memberships?licenseId=Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMWNjYmJjMTctZDYxNi00ZDc0LTg2NGItYjFmM2IwNzAxZmJhOk1TXzAzMDRjMDkzLTFjM2MtNDRlMC1iYjBhLWU1ZDE2NDM2NmQ1OQ&personId=Y2lzY29zcGFyazovL3VzL1BFT1BMRS8wZWZiNWVkMC0wY2FmLTRiNTYtYmMxMS03MzhlOWRhMDU5MjM`

```json
{
  "items" : [ {
    "id" : "Y2lzY29zcGFyazovL3VzL1JFU09VUkNFX0dST1VQX01FTUJFUlNISVAvcGVyc29uSWQ6bGljZW5zZUlk",
    "resourceGroupId" : "Y2lzY29zcGFyazovL3VzL1JFU09VUkNFX0dST1VQL2RlZmF1bHQ",
    "licenseId" : "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMWNjYmJjMTctZDYxNi00ZDc0LTg2NGItYjFmM2IwNzAxZmJhOk1TXzAzMDRjMDkzLTFjM2MtNDRlMC1iYjBhLWU1ZDE2NDM2NmQ1OQ",
    "personId" : "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8wZWZiNWVkMC0wY2FmLTRiNTYtYmMxMS03MzhlOWRhMDU5MjM",
    "personOrgId" : "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGUxMGY",
    "status" : "activated"
  } ]
}
```

#### 5. Assign User to the Resource Group

Use the [Update a Resource Group Membership endpoint](https://developer.webex.com/docs/api/v1/resource-group-memberships/update-a-resource-group-membership) to change the Resource Group for the user. Use the value of the new Resource Group created above for the `resourceGroupId` parameter.

`PUT https://webexapis.com/v1/resourceGroup/memberships/Y2lzY29zcGFyazovL3VzL1JFU09VUkNFX0dST1VQX01FTUJFUlNISVAvcGVyc29uSWQ6bGljZW5zZUlk`

```json
{
  "resourceGroupId" : "Y2lzY29zcGFyazovL3VzL1JFU09VUkNFX0dST1VQLzFjY2JiYzE3LWQ2MTYtNGQ3NC04NjRiLWIxZjNiMDcwMWZiYQ",
  "licenseId" : "Y2lzY29zcGFyazovL3VzL0xJQ0VOU0UvMWNjYmJjMTctZDYxNi00ZDc0LTg2NGItYjFmM2IwNzAxZmJhOk1TXzAzMDRjMDkzLTFjM2MtNDRlMC1iYjBhLWU1ZDE2NDM2NmQ1OQ",
  "personId" : "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8wZWZiNWVkMC0wY2FmLTRiNTYtYmMxMS03MzhlOWRhMDU5MjM",
  "personOrgId" : "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGUxMGY",
  "status" : "activated"
}
```

See [Cisco Webex Hybrid Services](https://www.cisco.com/c/en/us/solutions/collaboration/webex-hybrid-services/index.html) for background.
