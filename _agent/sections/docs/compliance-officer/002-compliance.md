---
type: Excerpt
canonical_url: https://developer.webex.com/docs/compliance-officer
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Compliance
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/compliance-officer). [Full Markdown](../../../../docs/compliance-officer.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Compliance Officers can access and manage organization content with dedicated authorization scopes. Learn how data ownership, room permissions, and meeting recordings affect that access.

## Selected section

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
