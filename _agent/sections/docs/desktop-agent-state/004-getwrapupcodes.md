---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-agent-state
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Desktop Actions
- getWrapUpCodes()
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

### getWrapUpCodes()

**Deprecated since January 16, 2025:** Use [fetchPaginatedAuxCodes](https://developer.webex.com/docs/desktop-agent-state#fetchpaginatedauxcodes) to retrieve auxiliary codes.

Retrieves the wrap up codes. Example: Credit Card Issue, Medical Query, Sales Explained.

**Example**

```javascript
const wrapUpCodes = await Desktop.actions.getWrapUpCodes()
// => Get current wrapUpCodes from Desktop store
// Retrieves configured wrap-up codes, such as "Credit Card Issue" or "Medical Query".
```

**Returns**

`{Array}` The array of objects.

**Example Response**

```javascript
const codes = [
{
    id: "2063",
    isDefault: false,
    isSystem: false,
    name: "Account Information Explained"
}, {
    id: "2061",
    isDefault: false,
    isSystem: false,
    name: "Credit Card Issue"
}
];
```
