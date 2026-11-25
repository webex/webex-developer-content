---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-agent-state
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Desktop Actions
- getIdleCodes()
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

### getIdleCodes()

**Deprecated since January 16, 2025:** Use [fetchPaginatedAuxCodes](https://developer.webex.com/docs/desktop-agent-state#fetchpaginatedauxcodes) to retrieve auxiliary codes.

Retrieves the current idle codes. Example: Idle, Coffee break, Meeting, Tea.

**Example**

```javascript
const idleCodes = await Desktop.actions.getIdleCodes();
// => Get current idleCodes from Desktop store
```

**Returns**
`{Array}` The array of objects.

**Example Response**

```javascript
const codes = [
{
    id: "1643",
    isDefault: false,
    isSystem: true,
    name: "RONA"
}, {
    id: "1644",
    isDefault: true,
    isSystem: false,
    name: "Meeting"
}
];
```
