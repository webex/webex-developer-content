---
type: Guide
title: Compliance Officer & Data Access
display_title: Compliance Officer & Data Access
canonical_url: https://developer.webex.com/docs/compliance-officer
content_type: documentation
product_group:
- webex-suite
categories:
- compliance
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/compliance-officer)

Compliance Officers can access and manage organization content with dedicated authorization scopes. Learn how data ownership, room permissions, and meeting recordings affect that access.

## Webex Data

### Permissions & Ownership

Data created within Webex belongs to the [organization](https://developer.webex.com/docs/api/v1/organizations) that owns the room (space). The owner of a group room is generally the organization for the person who created the room. For 1:1 rooms between users in different organizations, the organization that each person belongs to owns their participant’s content. Rooms created by bots are owned by the organization of the first non-bot participant.

Data access permissions within Webex vary depending on a few factors: the room creator, room membership, and organization membership. When a room is created, the organization associated with the creator is considered the **owning organization** for the room. If users from other organizations are added to the room, those organizations are **participating organizations** in the room.

In general, the following types of users will be viewing, creating, and managing data within Webex:

- Room participants—can send and view messages within the room.
- Room moderator—users can be assigned as a moderator by a room owner and have exclusive control of the room including the room’s title and participant list.
- Compliance officers for the owning organization—can monitor and manage all data within group rooms created by a member of the organization; can manage all content in 1:1 rooms, including those with external participants.
- Compliance officers for the participating organization-can monitor and manage data created by their users in rooms owned by another organization; can manage all content in 1:1 rooms with external participants.



> **Info**
>
> In a 1:1 room between users of different organizations, either organization’s compliance officers can monitor and manage data created by _both_ participants.



### Security & Privacy

A key management server (KMS) is responsible for the creation and security of the encryption keys the Webex clients use to encrypt and decrypt data and communications. It is architecturally and operationally separated from the rest of the Webex Cloud and its data is not accessible by any other components. Whether the KMS is managed by Cisco or installed and managed on-premise, data within the Webex Cloud is encrypted from end-to-end and is not decrypted until it reaches the API endpoint.

For more information about data security and privacy in Webex, please see the [Webex Security White Paper](https://www.cisco.com/c/dam/en/us/solutions/collateral/collaboration/cloud-collaboration/cisco-spark-security-white-paper.pdf).

## Compliance

### Compliance Officer

The role of a compliance officer is to ensure that a company is conducting its business in full compliance with all laws and regulations that pertain to its particular industry, as well as professional standards, accepted business practices, and internal standards.

The Webex REST API has compliance authorization scopes that support the compliance officer’s role. Using these `spark-compliance` scopes, compliance officers will have access to, and the ability to manage, all data created by their organization such as messages or content attachments. Compliance officers can monitor data and take action to mitigate compliance issues that could arise.

### Authorization Scopes

The `spark-compliance` scopes and their descriptions are listed below:



The scope catalog for category `compliance` is generated dynamically. View the [official portal page](<https://developer.webex.com/docs/compliance-officer>) for scope names and descriptions.



For instructions on how to add these scopes to your app and for a full list of all available authorization scopes see the [Integrations/OAuth Guide](https://developer.webex.com/docs/integrations).

### Using the Compliance Scopes

Normally, Webex REST API users only have access to information related to their account, such as messages in rooms where they are members. The `spark-compliance` scopes provide access to information across the organization. For instance, if granted the `spark-compliance:messages_read` scope, messages will be available for all rooms within the organization, not just those that the authenticated compliance officer is a member of.

Several scopes provide access to write data or take action within an organization. If an action should be taken against certain data within Webex for compliance reasons, the Webex REST API can be used with an authentication token authorized with one of the above scopes to carry out the action. For example, if a message needs to be deleted, the `spark-compliance:messages_write` scope will be required. To delete the message, use the [DELETE /messages endpoint](https://developer.webex.com/docs/api/v1/messages/delete-a-message). Similarly, if a member of a room, either a person or a bot, needs to be added or removed, the `spark-compliance:memberships_write` scope will be required and the membership can be deleted with the [DELETE /memberships endpoint](https://developer.webex.com/docs/api/v1/memberships/delete-a-membership).

When using the appropriate `spark-compliance:` scopes and API endpoints, the authenticated user *does not* need to be a member of the room to take action. For example, a compliance officer who is not a member of a particular room can create, update, or delete the room's [memberships](https://developer.webex.com/docs/api/v1/memberships) with the `spark-compliance:memberships_write` scope.

## Meetings

Please refer to the [Meetings](https://developer.webex.com/docs/meetings) documentation for details.

### Meeting Recordings

Compliance officers are able to retrieve user recordings for analysis and compliance. There is a separate API endpoint for admins and compliance officers [/admin/recordings](https://developer.webex.com/docs/api/v1/recordings/list-recordings-for-an-admin-or-compliance-officer), while regular users use [/recordings](https://developer.webex.com/docs/api/v1/recordings/list-recordings). As it relates to recording deletion, a recycle bin and associated recording `status` is available. A user typically moves a recording to the recycle bin via the GUI and then either restores the recording or purges the recording from the recycle bin. Once purged, the recording isn't accessible to regular users any longer, but it is still accessible to the Compliance Officer until it is removed through the retention process. Compliance officers who want to retrieve user-deleted recordings must query the [/events API](https://developer.webex.com/docs/api/v1/events) for deleted recording events, and use the returned recording ID to retrieve the recording from [/recordings/{id}](https://developer.webex.com/docs/api/v1/recordings/get-recording-details). Regular users will see a 404 error.
