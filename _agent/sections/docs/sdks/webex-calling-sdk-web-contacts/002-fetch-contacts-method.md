---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-contacts
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Fetch Contacts Method
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-contacts). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-contacts.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Calling SDK consists of various modules which are created at the time of its initialization. Among these integral modules, one noteworthy component is the `ContactClient`.

---

For an introduction, we recommend consulting our [Quickstart guide](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) which will walk you through the step-by-step process of creating a calling instance and provide insights into the instantiation of various modules.

By the end of this article, you will have a solid grasp of how to leverage `ContactClient` to enhance your application's calling capabilities and create a seamless user experience.

## Selected section

## Fetch Contacts Method

The `getContacts()` method retrieves the contacts and respective contact groups for a user.

```javascript
const contactListResponse = await contacts.getContacts();
```



|                |                                               |
| -------------- | --------------------------------------------- |
| **Parameters** | --                                            |
| **Returns**    | `Promise<ContactResponse>` |

### FetchContact Response

Here's the prototype for the response returned by the `getContacts()` method:

```javascript
{
  statusCode: number;
  data: {
    contacts?: Contact[];
    groups?: ContactGroup[];
    contact?: Contact;
    group?: ContactGroup;
    error?: string;
  };
  message: string | null;
};
```

Here's an example response for the `getContacts()` method:



> **Info**
>
> Only `contacts` and `groups` attributes are present.



```json
{
  "statusCode": 200,
  "data": {
    "contacts": [
      {
        "meta": {
          "created": "2023-08-31T13:19:15.631Z",
          "lastModified": "2023-08-31T13:19:15.631Z"
        },
        "contactId": "bd8c0601-e2d6-48ff-8559-72fec60131ad",
        "contactType": "CUSTOM",
        "avatarUrlDomain": "avatar-prod-us-east-2.webexcontent.com",
        "displayName": "John Doe",
        "phoneNumbers": [
          {
            "type": "work",
            "value": "1232323"
          }
        ],
        "encryptionKeyUrl": "kms://cisco.com/keys/ed180173-04ac-****-****-a9f0155f902f",
        "isMigration": false,
        "ownerId": "a126d98a-6570-487b-87a5-933dd3e97539",
        "groups": ["f5d524df-3479-43c6-a7fd-5fab47b87cab"]
      }
    ],
    "groups": [
      {
        "meta": {
          "created": "2021-05-05T09:39:35.067Z",
          "lastModified": "2021-05-05T09:39:35.067Z"
        },
        "groupId": "1b2af605-de8a-469f-b5ba-9becdae8b67d",
        "groupType": "NORMAL",
        "ownerId": "a126d98a-6570-487b-87a5-933dd3e97539",
        "displayName": "Other contacts",
        "encryptionKeyUrl": "kms://cisco.com/keys/ed180173-04ac-415f-8665-a9f0155f902f",
        "isMigration": false
      }
    ]
  },
  "message": "SUCCESS"
}
```



> **Info**
>
> If a user doesn't have any groups associated with their account, the SDK creates a default group name, "Other contacts".
