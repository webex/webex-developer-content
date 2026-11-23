---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-agent-state
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Desktop Actions
- fetchPaginatedAuxCodes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-agent-state). [Full Markdown](../../../../docs/desktop-agent-state.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Read agent information and manage availability by media channel with the Desktop SDK.

## Parent context

## Desktop Actions

Auxiliary-code pagination uses `Desktop.agentConfigJsApi`. The other methods in this section use `Desktop.actions`.

## Selected section

### fetchPaginatedAuxCodes

- Retrieves the current idle codes or the current wrap up codes. 
- Example for idle codes: `Idle`, `Coffee break`, `Meeting`, `Tea`.
- Example for wrapup codes: `Credit Card Issue`, `Medical Query`, `Sales Explained`.

**Example**
Fetch Idle codes : 

```javascript
const idleCodes = await Desktop.agentConfigJsApi.fetchPaginatedAuxCodes(
  {
    workType:"IDLE_CODE", // or "WRAP_UP_CODE"
    page: 0,
    pageSize: 100,
    search: "",
    customFilter: ""
  }
);// => Get page 0 of 100 idleCodes from Desktop
```

**Parameters**

| Name      | Type   | Description                                                                                                                                                                        | Required |
| --------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| workType | String | Specifies the required auxillary code is a wrapup code or an idle code.                                                                                                                                             | Yes      |
| page | number | Fetch details for the particular page number.                                                                                                                                            | No      |
| pageSize | number | Fetch the total number of items presant in one page.                                                                                                                                            | No      |
| search | String | Pass the search parameter.                                                                                                                                            | No      |
| customFilter | String | String that contains conditions for further filtering the results. This is based on the [rsql syntax](https://github.com/perplexhub/rsql-jpa-specification#rsql-syntax-reference).                                                                                                                                            | No      |

**Returns**
```json
{
    "meta": {
        "orgid": "58f1a59e-245c-4536-9ee4-06560658e493",
        "page": 0,
        "pageSize": 100,
        "totalPages": 10,
        "totalRecords": 910,
        "links": {
            "next": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active%3D%3Dtrue;workTypeCode%3D%3DIDLE_CODE&attributes=id,isSystemCode,name,defaultCode&desktopProfileFilter=true&page=1&pageSize=100&sort=name,asc",
            "last": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active%3D%3Dtrue;workTypeCode%3D%3DIDLE_CODE&attributes=id,isSystemCode,name,defaultCode&desktopProfileFilter=true&page=9&pageSize=100&sort=name,asc",
            "self": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active==true;workTypeCode==IDLE_CODE&attributes=id,isSystemCode,name,defaultCode&page=0&pageSize=100&desktopProfileFilter=true&sort=name,ASC",
            "first": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active%3D%3Dtrue;workTypeCode%3D%3DIDLE_CODE&attributes=id,isSystemCode,name,defaultCode&desktopProfileFilter=true&page=0&pageSize=100&sort=name,asc"
        }
    },
    "data": [
        {
            "isSystem": false,
            "name": "A_idleTest",
            "id": "6d686095-80df-4286-8b41-0a937990c905",
            "isDefault": true
        },
        {
            "isSystem": false,
            "name": "Break",
            "id": "3c5fa5f2-21fe-41cb-a5a3-5d71eccd5e1a",
            "isDefault": false
        }
    ]
}
```
Fetch wrap up codes :
```javascript
const wrapUpCodes = await Desktop.agentConfigJsApi.fetchPaginatedAuxCodes(
  {
    workType:"WRAP_UP_CODE",
    page: 0,
    pageSize: 100,
    search: "",
    customFilter: ""
  }
); 
// => Get page 0 of 100 of wrapUpCodes from Desktop
```
**Returns**
```json
{
    "meta": {
        "orgid": "58f1a59e-245c-4536-9ee4-06560658e493",
        "page": 0,
        "pageSize": 100,
        "totalPages": 3,
        "totalRecords": 211,
        "links": {
            "next": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active%3D%3Dtrue;workTypeCode%3D%3DWRAP_UP_CODE&attributes=id,isSystemCode,name,defaultCode&desktopProfileFilter=true&page=1&pageSize=100&sort=name,asc",
            "last": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active%3D%3Dtrue;workTypeCode%3D%3DWRAP_UP_CODE&attributes=id,isSystemCode,name,defaultCode&desktopProfileFilter=true&page=2&pageSize=100&sort=name,asc",
            "self": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active==true;workTypeCode==WRAP_UP_CODE&attributes=id,isSystemCode,name,defaultCode&page=0&pageSize=100&desktopProfileFilter=true&sort=name,ASC",
            "first": "/organization/58f1a59e-245c-4536-9ee4-06560658e493/v2/auxiliary-code?filter=active%3D%3Dtrue;workTypeCode%3D%3DWRAP_UP_CODE&attributes=id,isSystemCode,name,defaultCode&desktopProfileFilter=true&page=0&pageSize=100&sort=name,asc"
        }
    },
    "data": [
        {
            "isSystem": false,
            "name": "Break",
            "id": "fc4cae32-0b5f-4409-ad19-7ff570f68f20",
            "isDefault": false
        },
        {
            "isSystem": false,
            "name": "Customer Disconnected",
            "id": "cd0110c9-3fb5-4cf8-937f-e8fa55d46d01",
            "isDefault": true
        }
    ]
}
```
