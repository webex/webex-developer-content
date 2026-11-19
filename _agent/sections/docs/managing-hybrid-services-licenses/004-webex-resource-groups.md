---
type: Excerpt
canonical_url: https://developer.webex.com/docs/managing-hybrid-services-licenses
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Webex Resource Groups
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/managing-hybrid-services-licenses). [Full Markdown](../../../../docs/managing-hybrid-services-licenses.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex API includes several methods which can be used by administrators to programmatically manage license usage of Webex Hybrid Services.

## Selected section

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
