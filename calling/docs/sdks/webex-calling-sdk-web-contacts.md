---
type: Guide
title: Web Calling SDK | Contacts
display_title: Contacts
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-contacts
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-contacts)

The Calling SDK consists of various modules which are created at the time of its initialization. Among these integral modules, one noteworthy component is the `ContactClient`.

---

For an introduction, we recommend consulting our [Quickstart guide](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) which will walk you through the step-by-step process of creating a calling instance and provide insights into the instantiation of various modules.

By the end of this article, you will have a solid grasp of how to leverage `ContactClient` to enhance your application's calling capabilities and create a seamless user experience.

## Instantiate the ContactClient

The `ContactsClient` is implemented as the `ContactsClient` class in the SDK and there are two ways of instantiating it.

To instantiate just the `ContactsClient`, use the `createContactsClient` method:

```javascript
const contacts = createContactsClient(webex, logger);
```

If the `ContactsClient` is initialized through the `calling` instantiation:

```javascript
const contacts = calling.contactClient;
```

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

## Contacts Group API

The methods in this section let you perform operations on groups of contacts.

### Create Contact Group Method

The `createContactGroup()` creates a new contact group. A contact must belong to a group. You only need to specify the `groupName` for basic usage.

#### ContactGroup Object

Once the contact group is created using the `createContactGroup()` method, the `ContactGroup` object contains the following attributes:



| **Name** | **Description** | **Values** |
| --- | --- | --- |
| `displayName` | Display name for the group. | `string` |
| `encryptionKeyUrl` | `EncryptionKeyUrl` for the content key. | `string` |
| `groupId` | Group ID. | string |
| `groupType` | Group Type of contact, NORMAL, or EXTERNAL. Default: `NORMAL` | GroupType: `NORMAL`, `EXTERNAL` |
| `members` | String array of `contactId` s that are part of the group. | `string [ ]` |
| `ownerId` | Owner ID of the user. | `string` |

```javascript
const contactGroupCreatedResponse = await contacts.createContactGroup(displayName);
```



<table>
  <colgroup>
    <col style="width: 12%" />
    <col style="width: 88%" />
  </colgroup>
  <tbody>
    <tr>
      <td><strong>Parameters</strong></td>
      <td>
        Options
        
          <table>
            <tbody>
              <tr>
                <th style="width: 15%">Name</th>
                <th style="width: 40%">Description</th>
                <th style="width: 30%">Values</th>
                <th style="width: 15%">Required</th>
              </tr>
              <tr>
                <td><code>displayName</td>
                <td>Display name for group<br /><br /></td>
                <td>
                    <strong>string</strong>
                </td>
                <td>Yes</td>
              </tr>
              <tr>
                <td>
                  <code>encryptionKeyUrl
                </td>
                <td>
                  <code>EncryptionKeyUrl for the content key to be used.
                </td>
                <td>
                    <strong>string</strong>
                </td>
                <td>No</td>
              </tr>
              <tr>
                <td><code>groupType</td>
                <td>
                  Group Type of the contact either NORMAL or EXTERNAL. Default: <strong>NORMAL</strong>
                </td>
                <td>
                    <strong>GroupType</strong>
                  
                    <table>
                      <tbody>
                        <tr>
                          <th><strong>NORMAL</strong></th>
                          <th><strong>EXTERNAL</strong></th>
                        </tr>
                      </tbody>
                    </table>
                  
                </td>
                <td>No</td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td colspan="1">
        <strong>Returns</strong>
      </td>
      <td colspan="1">
            <strong>Promise&lt;ContactResponse&gt;</strong>
      </td>
    </tr>
  </tbody>
</table>

Here's an example of a response upon the successful creation of a group:

```javascript
{
    "statusCode": 201,
    "data": {
        "group": {
            "meta": {
                "created": "2023-09-05T08:27:32.651Z",
                "lastModified": "2023-09-05T08:27:32.651Z"
            },
            "groupId": "abf9ffd2-dab8-41c0-a28d-2c00426c5717",
            "groupType": "NORMAL",
            "ownerId": "a126d98a-6570-487b-87a5-933dd3e97539",
            "displayName": "testGRP",
            "encryptionKeyUrl": "kms://cisco.com/keys/ed180173-04ac-415f-8665-a9f0155f902f",
            "isMigration": false
        }
    },
    "message": "SUCCESS"
}
```

### Delete Contact Group

The `deleteContactGroup()` method lets you delete an existing contact group given a `groupId`.

```javascript
const groupId = '5b92c76b-42e2-4fa6-b14b-90b8be6913b6';

const contactGroupDeletedResponse = await contacts.deleteContactGroup(groupId);
```



|                |                                                 |
| -------------- | ----------------------------------------------- |
| **Parameters** | groupId                              |
| **Returns**    | `Promise<ContactResponse>` |

Here's an example of a response upon the successful deletion of a contact group.

```javascript
{
    statusCode: 204,
    data: {},
    message: SUCCESS,
};
```
