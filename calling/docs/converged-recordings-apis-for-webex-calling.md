---
type: Guide
title: Converged Recordings APIs for Webex Calling
display_title: Converged Recordings APIs for Webex Calling
canonical_url: https://developer.webex.com/docs/converged-recordings-apis-for-webex-calling
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/converged-recordings-apis-for-webex-calling)

The Webex Calling product recently added the option to have “Webex” be the call recording provider for an organization, alongside the previous set of third-party call recording partners. When selecting Webex as the call recording provider, it utilizes the same mechanism as Webex Meeting recordings to output high quality audio files.

---

Webex call recording is accessible to all users in a Calling organization and provides unlimited recording capabilities. Currently, Webex recordings have a retention period of one year, with each organization allotted 100GB of storage. Another great feature of Webex call recordings is the ability to receive [AI-generated summaries](https://help.webex.com/en-us/article/9leme/Webex-App-%7C-AI-generated-summaries-for-call-recordings), where you can quickly catch up on a discussion and get a better understanding of the conversation at a glance.

The Webex call recording option also gives developers access to a new set of APIs to automate the management of call recordings in Webex Calling – [Converged Recordings APIs](https://developer.webex.com/docs/api/v1/converged-recordings). These endpoints can be used for integrations that automate the archival of older recordings for long-term storage, satisfy compliance archival requirements, dynamically link conversations to customer profiles in a CRM, generate custom reports based on call recording metadata, route flagged recordings for supervisor review, and more.

In this article, we will first show how the Webex Call Recording option is selected in Control Hub. Then we will explore the new Converged Recordings API endpoints and explain how they work for different Webex user roles.

### Webex Call Recording in a Developer Sandbox

The first step to start using the Converged Recordings APIs is for an admin to enable Webex as the call recording provider for the organization. This is where a [Webex Developer Sandbox](https://developer.webex.com/admin/docs/developer-sandbox-guide) comes in handy, which provides administrator-level access to your own Webex organization. The instructions to enable Webex as the recording provider in Control Hub are rather straightforward:

1. Once you have access to a Developer Sandbox, log in to Control Hub with your admin credentials.
1. Go to *Services &gt; Calling &gt; Service Settings*.
1. Under **Call Recording**, select “Webex” as the call recording provider from the drop-down list.
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltfa64baabde6ef4bc/webex-calling-converged-recordings-api-blog-2.jpeg)
1. Click “Save”.

- For the most up to date instructions on enabling Webex call recording at an organizational level, see [these instructions](https://help.webex.com/en-us/article/ilga4/Manage-call-recording-for-Webex-Calling#Cisco_Task.dita_bdcfdaed-bd71-4a2e-a420-a43d2128f4c1).
- To configure your sandbox for call transcriptions (currently available only in the Webex app) and AI-generated summaries that includes Notes and Action Items (available on both the Webex app and Converged Recordings APIs), see [the instructions here](https://help.webex.com/en-us/article/ilga4/Manage-call-recording-for-Webex-Calling#concept-template_185f248b-c355-45ca-96ea-e44fe86340a8).

Since the developer sandboxes do not include public telephone access in Webex Calling, the easiest way to make test calls is by utilizing “extension dialing”.&#xa0; This allows calling between test users without the need for setting up a paid PSTN number. In this scenario, the calls are supported by Webex and not through the public telephone network. Test users can essentially be assigned any number string as a dialable extension. A test user can dial another user’s extensions, answer incoming calls, and execute in-call actions (including recording) [inside the Webex app](https://help.webex.com/en-us/article/n3xx7vcb/Get-started-with-Webex-App#Cisco_Concept.dita_117a2dd6-a84e-4247-a9fc-84a8d5644ee7) or by leveraging the [Call Control APIs](https://developer.webex.com/docs/api/v1/call-controls).

- For instructions on setting up extension dialing on a developer sandbox, [watch this helpful Vidcast](https://app.vidcast.io/share/974fc2b9-9ba1-4889-9d04-ea7751f92c33).
- To get more familiarized with the Call Control APIs, check out [my previous blog](https://developer.webex.com/blog/webex-calling-getting-started-with-call-control-apis) on this subject.

<br/>

### Exploring the Converged Recordings APIs

While the Webex Meetings and Calling products can share the same method of recording when Webex is selected as the call recording provider, the [Recording APIs](https://developer.webex.com/meeting/docs/api/v1/recordings) are still the exclusive to Meetings and Converged Recordings APIs are exclusive to Calling. In the future, Meeting Recordings will also be included in the Converged Recordings APIs. Until then, both sets of APIs do share the same basic schema that makes it easy to transition from one endpoint to the other.

In this section, we’ll break down the functionality for the Converged Recordings APIs based on specific roles in Webex.

#### User Level APIs

Integrations for *regular Webex users* have access to the following Converged Recordings APIs:

- [List Recordings](https://developer.webex.com/calling/docs/api/v1/converged-recordings/list-recordings) – *required scope is* `spark:recordings_read`

  - This endpoint is usually the first API call used to retrieve the `ID` that corresponds to a specific recording that is required for subsequent API calls. This API also returns some general data about the file and the available `status` of the file. If the `status` is specified as `deleted`, the recording has been moved to the *recycle bin*.

- [Get Recording Details](https://developer.webex.com/calling/docs/api/v1/converged-recordings/get-recording-details) – *required scope is* `spark:recordings_read`

  - This endpoint requires the `recordingID` that is retrieved from the *List Recordings API* noted priorly. This returns the unique download links for the call recordings, AI-generated summaries (action items, suggested notes, and short notes), along with other data of the recording file.

- [Get Recording metadata API](https://developer.webex.com/docs/api/v1/converged-recordings/get-recording-metadata) – *required scope is* `spark:recordings_read`

  - This endpoint requires a `recordingID` to retrieve the metadata of the recording file which contains much more details of the recording, including sensitive data such as phone numbers. If the query parameter showAllTypes is `true`, the additional details about `mediaStreams`, `participants`, `redirectInfo` and `redirectedCall` are included in the response body.
- [Move Recordings into the Recycle Bin](https://developer.webex.com/calling/docs/api/v1/converged-recordings/move-recordings-into-the-recycle-bin) – *required scope is* `spark:recordings_write`

  - This endpoint requires a `recordingID` to move individual recordings to the recycle bin (soft delete). To move all recordings of the user to the recycle bin, the `trashAll` parameter that is set to `true` can be added to the request body and no `recordingID`is required.

- [Purge Recordings from Recycle Bin](https://developer.webex.com/calling/docs/api/v1/converged-recordings/purge-recordings-from-recycle-bin) – *required scope is* `spark:recordings_write`

  - This endpoint requires a `recordingID` that has a `status` specified as `deleted` to purge individual recordings from the recycle bin (hard delete). To purge all recordings of the user from the recycle bin, the `purgeAll` parameter that is set to `true` can be added to the request body and no `recordingID`is required. Recordings are fully purged from the recycle bin only after the 30-day retention policy is met and cannot be restored after that. During the retention period, an admin or compliance officer can still restore recordings purged by the user.

- [Restore Recordings from Recycle Bin](https://developer.webex.com/calling/docs/api/v1/converged-recordings/restore-recordings-from-recycle-bin) – *required scope is* `spark:recordings_write`

  - This endpoint requires a `recordingID` that has a `status` specified as `deleted` to restore individual recordings from the recycle bin. To restore all recordings of the user from the recycle bin, the `restoreAll` parameter set to `true` can be added to the request body and no `recordingID`is required.

<br/>

#### Administrator and Compliance Officer Level APIs

Integrations for *Webex administrators* and *compliance officers* have access to larger set of Converged Recordings APIs, some of which are exclusive to either role:

- [List Recordings for Admin or Compliance Officer](https://developer.webex.com/calling/docs/api/v1/converged-recordings/list-recordings-for-admin-or-compliance-officer) –
*required scope for admin is* `spark-admin:recordings_read`,
*required scope for compliance officer is* `spark-compliance:recordings_read`

  - This endpoint works much like the List Recordings API for users to retrieve the `recordingID` for each file, except there are a variety of extra query parameters to filter by specific owners, dates, locations, etc.

- [Get Recording Details](https://developer.webex.com/calling/docs/api/v1/converged-recordings/get-recording-details) –
*required scope for admin is* `spark-admin:recordings_read`,
*required scope for compliance officer is* `spark-compliance:recordings_read`

  - This endpoint requires the `recordingID` that is retrieved from the *List Recordings for Admin or Compliance Officer API* noted priorly. This returns the unique download links along with other data of the recording file.

- [Get Recording metadata API](https://developer.webex.com/docs/api/v1/converged-recordings/get-recording-metadata) –
*required scope for admin is* `spark-admin:recordings_read`,
*required scope for compliance officer is* `spark-compliance:recordings_read`

  - Just like the user level scope, this endpoint requires a `recordingID` to retrieve the metadata of the recording file which contains much more details of the recording, including PII data. If the query parameter showAllTypes is true, the additional details about `mediaStreams`, `participants`, `redirectInfo` and `redirectedCall` are included in the response body.
- [Move Recordings into the Recycle Bin](https://developer.webex.com/calling/docs/api/v1/converged-recordings/move-recordings-into-the-recycle-bin) – *required scope for admin is* `spark-admin:recordings_write`

  - Just like the user level scope, this endpoint requires a `recordingID` to move individual recordings to the recycle bin (soft delete). To move all recordings of the user to the recycle bin, the `trashAll` parameter that is set to `true` can be added to the request body. In this case, an `ownerEmail` is now required and a `recordingID`is not.

- [Purge Recordings from Recycle Bin](https://developer.webex.com/calling/docs/api/v1/converged-recordings/purge-recordings-from-recycle-bin) – *required scope for admin is* `spark-admin:recordings_write`

  - Just like the user level scope, this endpoint requires a `recordingID` that has a `status` specified as `deleted` to purge individual recordings from the recycle bin (hard delete). To purge all recordings of the user from the recycle bin, the `purgeAll` parameter that is set to `true` can be added to the request body. In this case, an `ownerEmail` is now required and a `recordingID`is not. Recordings are fully purged from the recycle bin only after the 30-day retention policy is met and cannot be restored after that. See the [Compliance Guide](https://developer.webex.com/compliance/docs/compliance) for more information on recording file retention policy.

- [Restore Recordings from Recycle Bin](https://developer.webex.com/calling/docs/api/v1/converged-recordings/restore-recordings-from-recycle-bin) – *required scope for admin is* `spark-admin:recordings_write`

  - Just like the user level scope, this endpoint requires a `recordingID` that has a `status` specified as `deleted` to restore individual recordings from the recycle bin. To restore all recordings of the user from the recycle bin, the `restoreAll` parameter that is set to `true` can be added to the request body. In this case, an `ownerEmail` is now required and a `recordingID`is not.

- [Reassign Recordings](https://developer.webex.com/calling/docs/api/v1/converged-recordings/reassign-recordings) – *required scope is* `spark-admin:recordings_write`

  - This endpoint is **exclusive toadministrators** and requires two parameters: `reassignOwnerEmail` for the account the recordings will be moved into, and `recordingIds` which accepts a list of one or more `recordingID` values that specify the files to be reassigned.

- [Delete a Recording](https://developer.webex.com/calling/docs/api/v1/converged-recordings/delete-a-recording) – *required scope is* `spark-compliance:recordings_write`

  - This endpoint is **exclusive to compliance officers** and requires a `recordingID` to permanently delete a call recording. Once a recording is deleted by a compliance officer, it becomes inaccessible no matter the user role and purged from Webex altogether.
