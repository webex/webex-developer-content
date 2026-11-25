---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-outbound-callbacks
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Address Books and Outbound ANI
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-outbound-callbacks). [Full Markdown](../../../../docs/desktop-outbound-callbacks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Initiate outbound calls, update call-associated data, and manage scheduled callbacks with the Desktop SDK.

## Selected section

## Address Books and Outbound ANI

These methods belong to `Desktop.agentStateInfo`.

### fetchAddressBooks()

Retrieves the address book details.

**Example**

```javascript
const books = await Desktop.agentStateInfo.fetchAddressBooks();
```

**Returns**
`{Object}` The address book response. Its `speedDials` property is an array of address entries.

**Example Response**

```javascript
const addressBooks = {
    speedDials: [{
            desc: 'Jane Doe',
            dn: '9997770094'
        },
        {
            desc: 'John Doe',
            dn: '9997770095'
        },
    ]
};
```

**Address type**

```typescript
type Address = {
    desc: string;
    dn: string;
    phoneBookName ? : string;
};
```

### mockOutdialAniList()

Fetches the ANI list that is used for an outdial call. The administrator adds the outdial ANI list to an agent profile. The outdial number is used as the caller number, and is displayed to the customer as the caller ID.
Updates the store variable value as per the response received from `mockOutdialAniList`. (Initially the store variable value will be empty).

**Store Variable**

```javascript
STORE.agent.outdialAniList
```

**Example**

```javascript
await Desktop.agentStateInfo.mockOutdialAniList();
```

**Returns**
`{Object}` Lists the outdial ANI.

**Example Response**

```javascript
const mockOutdialAniListResponse = {
  data: {
    agentSessionId: "",
    callData: "",
    data: {
      mockOutdialAniList: [
        {
          id: "+1-3364112001",
          name: "outdial ani"
        },
        {
          id: "+1-3364112002",
          name: "outdial ani two"
        },
        {
          id: "+1-3364112003",
          name: "outdial ani three"
        },
        {
          id: "+1-3364112004",
          name: "outdial ani four"
        }
      ]
    },
    jsMethod: "mockOutdialAni"
  },
  orgId: "b33fb142-4d65-4781-9899-19b0363cd45f",
  trackingId: "notifs_b3cf873d-56e4-4f6b-801d-c0dc49f3dd87",
  type: "mockOutdialAniList"
};
```
