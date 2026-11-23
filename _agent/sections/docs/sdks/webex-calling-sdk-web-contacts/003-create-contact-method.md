---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-contacts
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Create Contact Method
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-contacts). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-contacts.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Calling SDK consists of various modules which are created at the time of its initialization. Among these integral modules, one noteworthy component is the `ContactClient`.

---

For an introduction, we recommend consulting our [Quickstart guide](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) which will walk you through the step-by-step process of creating a calling instance and provide insights into the instantiation of various modules.

By the end of this article, you will have a solid grasp of how to leverage `ContactClient` to enhance your application's calling capabilities and create a seamless user experience.

## Selected section

## Create Contact Method

This API helps to create the contact for the user. There are two ways to create contacts.

1. **CUSTOM** - These are the contacts created by a user manually that are not present in a user's organization.
2. **CLOUD** - These are Directory Contacts from the user's organization.



| Operation                      | Contact Type | Required Parameters          |
| ------------------------------ | ------------ | ---------------------------- |
| Creating Personal contacts     | CUSTOM       | `displayName`, `contactType` |
| Adding Contacts from Directory | CLOUD        | `contactId`, `contactType`   |

This API accepts the Contact object as a parameter. It consists of various attributes covered in the following table:



| **Name** | **Description** | **Type** | **Required** |
| --- | --- | --- | --- |
| `addressInfo` | Address information. | `Address Type { }` | No |
| `avatarURL` | Avatar URL | `string` | No |
| `avatarUrlDomain` | Domain of Avatar URL. | `string` | No |
| `companyName` | Company name of the contact. | `string` | No |
| `contactId` | The `contactId` of the person. The same as a `userId` in the case of a CLOUD contact. | `string` | Required only for **CLOUD** |
| `contactType` | Type of contact, CUSTOM or CLOUD. | `ContactType` | Yes |
| `department` | Contact's department. | `string` | No |
| `displayName` | Display name for the group. | `string` | Required only for **CUSTOM** |
| `emails` | Email addresses of the contact. | `[]` | No |
| `encryptionKeyUrl` | `EncryptionKeyUrl` for the content key to be used. | `string` | No |
| `firstName` | First Name | `string` | No |
| `groups` | Group IDs of the groups that the contact is part of. | `string[]` | Yes |
| `kmsResourceObjectUrl` | `kmsResourceObjectUrl` for the content Object to be used. | `string` | No |
| `lastName` | Last name | `string` | No |
| `manager` | Name of contact's manager | `string` | No |
| `ownerId` | `ownerId` of the user | `string` | No |
| `phoneNumbers` | PhoneNumbers | `[]` | No |
| `primaryContactMethod` | Primary contact method as set by the contact/person. | `string` | No |
| `sipAddresses` | List of SIP addresses. | `[]` | No |
| `title` | Job title of the person/contact. | `string` | No |

### Define a contactInfo Object and Create a Contact

You can define a `contactInfo` object as either a `CLOUD` or a `CUSTOM` contact. Once you've created the `contactInfo` object, pass it to the `createContact()` method:

```javascript
// For a CLOUD contact

const contactinfo = {
  contactId: '<UUID>',
  contactType: 'CLOUD'
};

// For a CUSTOM contact

const contactinfo = {
  displayName: 'John Doe',
  contactType: 'CUSTOM',
  phoneNumber: [
    {
      type: 'work',
      value: '+1987987521'
    }
  ]
};
const contactCreatedResponse = await contacts.createContact(contactInfo);
```


|                |                                               |
| -------------- | --------------------------------------------- |
| **Parameters** | contactInfo     |
| **Returns**    | `Promise<ContactResponse>` |

Here's an example of a response after a contact is successfully created (in this case, a `CUSTOM` contact):

```javascript
{
  "statusCode": 201,
  "data": {
    "contact": {
      "avatarURL": "",
      "displayName": "testuser1",
      "phoneNumbers": [
        {
          "type": "work",
          "value": "+1985557521"
        }
      ],
      "contactType": "CUSTOM",
      "encryptionKeyUrl": "kms://cisco.com/keys/ed180173-04ac-415f-8665-a9f0155f902f",
      "groups": [
        "1b2af605-de8a-469f-b5ba-9becdae8b67d"
      ],
      "schemas": "urn:cisco:codev:identity:contact:core:1.0",
      "contactId": "48db494a-f23a-42b3-88e7-830ee31db7ae"
    }
  },
  "message": "SUCCESS"
}
```



> **Info**
>
> If a `contact.group` is not defined, the default group **Other contacts** is used.



### Delete a Contact Method

The `deleteContact()` method lets you delete a contact. It takes a `contactId` as an argument.

```javascript
const contactId = 'bd8c0601-e2d6-48ff-8559-72fec60131ad';

const contactDeletedResponse = await contacts.deleteContact(contactId);
```



|                |                                                 |
| -------------- | ----------------------------------------------- |
| **Parameters** | contactId                            |
| **Returns**    | `Promise<ContactResponse>` |

Here's an example of a response from a successful contact deletion:

```javascript
{
    statusCode: 204,
    data: {},
    message: SUCCESS,
};
```
