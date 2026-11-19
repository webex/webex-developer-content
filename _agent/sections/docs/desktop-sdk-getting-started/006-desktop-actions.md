---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-sdk-getting-started
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Desktop Actions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-sdk-getting-started). [Full Markdown](../../../../docs/desktop-sdk-getting-started.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Install and initialize the Desktop SDK to access Desktop modules from custom widgets.

## Selected section

## Desktop Actions

The `Desktop.actions` module retrieves data and performs actions for Desktop widgets.

### getToken()

Retrieves the authentication token used for SSO authentication.

**Example**

```javascript
const accessToken = await Desktop.actions.getToken();
// => Get current accessToken from Desktop store
```

**Returns**
`{String}` A user access token.
