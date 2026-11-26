---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-contacts
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Contacts Group API
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-contacts). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-contacts.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Calling SDK consists of various modules which are created at the time of its initialization. Among these integral modules, one noteworthy component is the `ContactClient`.

---

For an introduction, we recommend consulting our [Quickstart guide](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) which will walk you through the step-by-step process of creating a calling instance and provide insights into the instantiation of various modules.

By the end of this article, you will have a solid grasp of how to leverage `ContactClient` to enhance your application's calling capabilities and create a seamless user experience.

## Selected section

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
