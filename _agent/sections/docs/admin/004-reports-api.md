---
type: Excerpt
canonical_url: https://developer.webex.com/docs/admin
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Reports API
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/admin). [Full Markdown](../../../../docs/admin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](003-authentication.md)

## Article introduction

Manage Webex users, licenses, and hybrid services programmatically with the Webex Admin APIs.

## Selected section

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
