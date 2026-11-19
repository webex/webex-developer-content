---
type: Guide
title: Webex Admin | Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/admin
content_type: documentation
product_group:
- webex-suite
categories:
- admin
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/admin)

Manage Webex users, licenses, and hybrid services programmatically with the Webex Admin APIs.

## What's Possible with Admin APIs

The Webex APIs include several APIs that allow administrators to programmatically perform administrative actions such as provisioning a user or assigning a license to a user. By automating administration, user management and provisioning can be performed from an existing tool, rather than using the [Webex Control Hub](https://admin.webex.com).

Using these APIs, an admin can, for example:

- [Create a user](https://developer.webex.com/docs/api/v1/people/create-a-person)
- [Update a user](https://developer.webex.com/docs/api/v1/people/update-a-person)
- [View license usage of an organization](https://developer.webex.com/docs/api/v1/licenses/get-license-details)
- [View available roles of an organization](https://developer.webex.com/docs/api/v1/roles/list-roles)
- [Manage Hybrid Services licenses and users](https://developer.webex.com/docs/managing-hybrid-services-licenses)
- [View information about Hybrid Clusters](https://developer.webex.com/docs/api/v1/hybrid-clusters) or [Hybrid Connectors](https://developer.webex.com/docs/api/v1/hybrid-connectors)



> **Warning**
>
> If your organization uses the [Cisco Directory Connector](https://www.cisco.com/go/hybrid-services-directory) to synchronize Webex user accounts with Active Directory accounts, then you cannot _create_ or _delete_ Webex users using the [People API](https://developer.webex.com/docs/api/v1/people). Additionally, the People API will not allow you to _update_ any attributes of your existing users that are being synchronized by the Directory Connector.



## Admin Audit Events

Full administrators for an organization can use the [Admin Audit Events API](https://developer.webex.com/docs/api/v1/admin-audit-events) to retrieve information about significant actions taken by administrators in Webex Control Hub. See [this article](https://help.webex.com/n3b0w6x/) for detailed information about the types of events you can retrieve.



> **Info**
>
> Administrators with accounts created before 2019 who have never logged into [Webex Control Hub](https://admin.webex.com/) will need to log into Webex Control Hub at least once to enable access to the [Admin Audit Events API](https://developer.webex.com/docs/api/v1/admin-audit-events).



## Authentication

Use of these APIs requires you to be an administrator of an organization. If you are not an administrator of an organization, but wish to develop against these APIs, see below for instructions on how to get administrator access to an Administration Sandbox organization.

If you are an administrator, log into this site to get a development auth token with the necessary scopes.

To create an [Integration](https://developer.webex.com/create/docs/integrations) that will act on behalf of an administrator, include one or more of the following scopes when requesting an auth token via OAuth:



The scope catalog for category `admin` is generated dynamically. View the [official portal page](<https://developer.webex.com/docs/admin>) for scope names and descriptions.



## Reports API

The [Webex Reports API](https://developer.webex.com/docs/api/v1/reports) is available for Organizations with [Pro Pack for Cisco Webex Control Hub](https://www.cisco.com/go/pro-pack). The `analytics:read_all` scope is required to work with reports.

Reports are only visible to the user who created the report.  Each user is limited to 50 reports. If a user tries to create more than 50 reports, an error will be returned by the API. See below for errors you may encounter from the API.

### Using the Reports API

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb39d7513c0c01b11/5f05c051e5f0487064a76689/Webex-Reports-Flow.png" width="744" height="152" title="Webex Reports Flow"></img>

1. [List Report Templates](https://developer.webex.com/docs/api/v1/report-templates)

    First, list the available report templates. These templates are available for you to use when creating a report.

2. [Create the Report](https://developer.webex.com/docs/api/v1/reports/create-a-report)

    Determine which template you want to use to create the report. Specify the date range for the report when creating it.

    After creating the report, make note of the `id` returned. This is the report's ID. You will need this later to download it.

3. [Check the Report's Status](https://developer.webex.com/docs/api/v1/reports/get-report-details)

    While the report is generated, you can check on the status of the report by retrieving the report with the ID you noted in the previous step.

4. [Download the Report](https://developer.webex.com/docs/api/v1/reports/get-report-details)

    When the report is ready, use the download link in the response to download the report. The maximum number of downloads is 30.
    

> **Info**
>
> Downloaded reports are automatically deleted after 24 hours following the final download.



5. [Delete the Report](https://developer.webex.com/docs/api/v1/reports/delete-a-report)

    Organizations may keep up to 50 reports at any time. After you've created and downloaded your report, delete it to make room for the next report.

### Reports API Errors

If you encounter an error when creating a report, the response will include an `ErrorCode`. See below for more information about the error.



|HTTP Code|ErrorCode|Description|
|---------|---------|-----------|
|400|1000|Reach the limit for creating reports|
|400|1001|Report Template ID not found|
|400|1002|Over the maximum date selection allow|
|400|1003|No access to sites that you do not belong to|
|400|1004|SiteUrl cannot be empty for site level template|
|400|1008|`reportId` does not exist|
|400|1009|[field required for validation, for example: templateId, siteList, etc ] can not be empty!|
|400|1016|Either none or both of `from` and `to` query parameter must be present in request|
|401|1010|Authorization token not provided|
|401|1011|Authorization token wrong or expired|
|401|1012|Feature toggle not enabled|
|401|1014|The user does not have allowed role|
|401|1018|CI Access Token or scope of the token is not valid!|
|403|1005|Not allow to generate ui report by api|
|403|1006|Not allow to delete others report|
|429|1007|Number of downloads for this report has reached the limit within 24 hrs|

## Developer Sandbox

If you would like to develop against the Admin APIs but you are not an administrator of your Webex Organization, you can [request a Developer Sandbox](https://developer.webex.com/docs/developer-sandbox-guide). A Developer Sandbox provides you with a Webex administrator account for a "dummy" organization you can use to develop and test bots, integrations, and embedded apps outside of your primary organization.

For more information and to request a Developer Sandbox organization see the [Developer Sandbox Guide](https://developer.webex.com/docs/developer-sandbox-guide).
