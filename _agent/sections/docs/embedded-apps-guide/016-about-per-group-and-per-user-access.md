---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- About Per-Group and Per-User Access
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-guide). [Full Markdown](../../../../docs/embedded-apps-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

The general approach to developing embedded apps is similar to developing any other web app.

---

The main difference is that your app runs within the context of a Webex Meeting or Space, rather than in an external web browser. Embedded apps integrate with the Embedded App Framework to enable the following features:

* Ability to start an "Open for all" session with Meeting participants, or "Add to Tab" functionality in a Space.
* Get information about the meeting or messaging space host and user information (if permitted by the user or organization), Webex or Meeting Center theme color (light or dark, for example), and other details.
* Respond to events emitted by the framework about changes to the app's environment (theme change, for example), changes to the meeting host or space , or display context (sidebar or pop-out window).



> **Success**
>
> As of Webex app version 44.3, we’ve integrated the Webex AppHub natively into the Webex app itself, allowing your users to explore Apphub to discover apps and bots without the need to leave the Webex application! For more information, see [What's New](https://developer.webex.com/docs/embedded-apps-whats-new).





> **Info**
>
> If you are not currently a Webex customer you can [request a developer sandbox](https://developer.webex.com/docs/developer-sandbox-guide) to start developing embedded apps. Free Webex user accounts cannot be used to create embedded apps.





> **Info**
>
> The Embedded Apps version 1 SDK has been deprecated and will be supported based upon the following [support policy](https://developer.webex.com/docs/webex-api-and-sdk-support-policy#current-end-of-life-eol-notices). For new customers accessing this page, please see the [Embedded Apps version 2 SDK API Reference](https://eaf-sdk.webex.com/). For existing version 1 SDK customers, please see [Migration from 1.x to 2.x](https://eaf-sdk.webex.com/#migration-from-1x-to-2x). New features will only be added to the version 2 SDK.



The basic workflow for developing embedded apps is as follows:

1. Create an embedded app in the [Webex Developer Portal](), providing the HTTPS URL of your app's starting page. At this point your app is in development mode is only visible to your Webex account.
2. [Enable Developer Tools](https://developer.webex.com/docs/embedded-apps-guide#enabling-developer-tools) in Meeting Center or Spaces so you can debug your app within the embedded context.
3. Open the app in a Meeting or Space to test it. Publish changes or fixes to your web host, and use the **Reload** menu item available the right-click/control-click context menu to reload your app's resources. In this way you can quickly iterate on changes directly in the Meeting or Space.

## Selected section

## About Per-Group and Per-User Access

By default, embedded apps that are approved for use in a Webex organization are available in the App Gallery to all users in that organization. Webex organization administrators can optionally enable an embedded app for a subset of users in the organization, on a per-user or per-group basis.

Currently, you can use Control Hub to [assign groups to embedded apps](https://developer.webex.com/docs/embedded-apps-guide#assigning-groups-to-embedded-apps) and the Groups API to [create groups and manage group members](https://developer.webex.com/docs/embedded-apps-guide#creating-and-managing-groups).

<a id="assigning-groups-to-embedded-apps"></a>

### Assigning Groups to Embedded Apps

Administrators use the [Embedded Apps control panel](https://admin.webex.com/apps/embeddedApps) in [Control Hub](https://admin.webex.com/) to view groups and their members, and to assign groups to an embedded app. You can assign groups to public apps and private apps. In-development apps that have not been approved for by an org admin can not be assigned to a group. You cannot create or manage groups using Control Hub at this time. See [Creating and Managing Groups](https://developer.webex.com/docs/embedded-apps-guide#creating-and-managing-groups).

**To assign one or more groups to an embedded app:**

1. Open the [Embedded Apps control panel](https://admin.webex.com/apps/embeddedApps) in [Control Hub](https://admin.webex.com). The account you use to sign into Control Hub must have administrator privileges.
2. Select the **Public** or **Private** tab, then select the app to which you want to assign a group.
3. For public apps, in the **Access** panel select the **Select groups** option. For private apps this option is found in the **Submission Status** panel for [approved applications](https://help.webex.com/en-us/article/y1eqyd/Embedded-apps-in-Webex#Cisco_Task_in_List_GUI.dita_embeddedapp1).
4. Select one or more groups from the list you want to assign to the app. Filter the list by typing the group name you want to apply.
5. Click **Done** when finished.

    For example, the following screenshots show groups being assigned to public and private apps.

    ![Control Hub user interface for assigning groups to public and private apps](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4c7875fbe5253126/62c75f4830ed0e3641c61566/public-private-groups.png)

<a id="creating-and-managing-groups"></a>

### Creating and Managing Groups

To create and manage groups you use the [Groups API](https://developer.webex.com/docs/api/v1/groups). To use this API your user must be an organization admin. To manage groups and their users an access token with the `identity:groups_rw` (Read Write groups) scope is required. Searching and viewing members of a group requires an access token with a scope of `identity:groups_read`.

* [Create a group](https://developer.webex.com/docs/api/v1/groups/create-a-group)
* [Update a group](https://developer.webex.com/docs/api/v1/groups/update-a-group)
* [Get Group Details](https://developer.webex.com/docs/api/v1/groups/get-group-details)

### Creating a Group

You use the [Create a Group](https://developer.webex.com/docs/api/v1/groups/create-a-group) endpoint to create a new group. For example, the following creates a new group named "Beta Group" with no members. Replace `<TOKEN>` with an access token associated with a Webex organization admin's account.

```plaintext
curl -d '{"displayName":"Beta Group"}' \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <TOKEN>' \
-X POST https://webexapis.com/v1/groups
```

The response contains information about the newly created group, including the number of members.

```javascript
{
  "id": "Y2lzY29zc....hNGQxZg",
  "displayName": "Beta Group",
  "orgId": "Y2lzY29z....YTRkMWY",
  "created": "2022-07-07T17:47:24.017Z",
  "lastModified": "2022-07-07T17:47:24.017Z",
  "memberSize": 0
}
```

To add members to a group when creating it you use the `members` parameter. This field takes an array of objects whose `id` field specifies the ID of the Webex users to add. You can use the the [List People](https://developer.webex.com/docs/api/v1/people/list-people) to query for users in your organization and obtain their IDs.

For example, the following creates a new group named "Beta Group" that contains a single member with ID `<PERSON_ID>`.

```plaintext
curl -d '{"displayName":"Beta Group", "members": [{"id":"<PERSON_ID>"}]}' \ 
-H 'Content-Type: application/json' \
-H "Authorization: Bearer <TOKEN>" \
-X POST https://webexapis.com/v1/groups
```

The response contains information about the new group, including a `members` array that lists the current members of the group.

```javascript
{
  "id": "Y2lzY2...NhNGQxZg",
  "displayName": "Beta Group",
  "orgId": "Y2lzY2...TRkMWY",
  "created": "2022-07-07T19:19:19.998Z",
  "lastModified": "2022-07-07T19:19:19.998Z",
  "memberSize": 1,
  "members": [
    {
      "id": "<PERSON_ID>",
      "type": "user",
      "displayName": "user1@example.com"
    }
  ]
}
```

### Updating a Group

To update a group, such as add or remove members, or change its name, you use the [Update a Group](https://developer.webex.com/docs/api/v1/groups/update-a-group) PATCH API. For example, the following adds a member with ID `<PERSON_ID>` to the group with ID `<GROUP_ID>`.

```plaintext
curl -d '{"members": [{"id":"<PERSON_ID>"}]}' \
-H 'Content-Type: application/json'  \
-H "Authorization: Bearer <TOKEN>" \
-X PATCH https://webexapis.com/v1/groups/<GROUP_ID>
```

The JSON response object contains the updated `members` array with the newly added member.

```javascript
{
  "id": "Y2lzY2...hNGQxZg",
  "displayName": "Beta Group",
  "orgId": "Y2lzY29z...TRkMWY",
  "created": "2022-07-07T22:00:27.231Z",
  "lastModified": "2022-07-07T22:07:38.143Z",
  "memberSize": 2,
  "members": [
    {
      "id": "Y2lzY29zc",
      "type": "user",
      "displayName": "user1@example.com"
    },
    {
      "id": "<PERSON_ID>",
      "type": "user",
      "displayName": "user2@example.com"
    }
  ]
}
```

By default, users in the members array are added to the specified group.  To delete a group member, add `"operation": "delete"` to the array object. For example, the following deletes a member with ID `<PERSON_ID>` from the group with ID `<GROUP_ID>`.

```plaintext
curl -d '{"members": [{"id":"<PERSON_ID>", "operation": "delete"}]}' \
-H 'Content-Type: application/json'  \
-H "Authorization: Bearer <TOKEN>" \
-X PATCH https://webexapis.com/v1/groups/<GROUP_ID>
```

Of course, you can combine `add` and `delete` operations in the same operation. The following deletes one member with ID `<PERSON_1_ID>` and adds another with ID `<PERSON_2_ID`> to the specified group.

```plaintext
curl -X PATCH https://webexapis.com/v1/groups/<GROUP_ID> \
-H 'Content-Type: application/json'  \
-H "Authorization: Bearer <TOKEN>" \
--data-binary @- <<BODY
{ 
    "members": [
        { "id": "<PERSON_1_ID>", "operation": "delete" },
        { "id": "<PERSON_2_ID", "operation": "add" }
    ] 
}
BODY
```
