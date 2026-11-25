---
type: Excerpt
canonical_url: https://developer.webex.com/docs/integration-scopes
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Important scope behavior
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/integration-scopes). [Full Markdown](../../../../docs/integration-scopes.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Select scopes](001-select-scopes.md) [Available scopes](002-available-scopes.md)

## Article introduction

Use this reference to select the minimum Webex Suite and Webex Contact Center scopes that your integration needs.

## Selected section

## Important scope behavior

### Administrative scopes

Scopes beginning with `spark-admin` require a user with administrative access to the organization. Requesting one of these scopes does not elevate the authorizing user's role.

For Webex Contact Center administrator APIs, the authorizing user must have the appropriate Webex Contact Center administrator role in Control Hub. See [Webex Contact Center administrator roles and privileges](https://help.webex.com/en-us/article/n5jdj19/Webex-Contact-Center-administrator-roles-and-privileges).

### Compliance scopes

Scopes beginning with `spark-compliance` require an organization compliance officer. See the [Compliance Guide](https://developer.webex.com/docs/compliance#compliance).

### `spark:all`

The `spark:all` scope grants access to Webex account features that are not covered by other user-level scopes. It does not include `spark-admin` privileges. Some Webex SDK calling features require `spark:all`; most integrations should request narrower scopes.

### `spark:kms`

Webex adds `spark:kms` to an integration's selected scopes so it can interact with encrypted content such as messages. The generated authorization URL includes this scope. If you build the authorization URL yourself, include `spark:kms` when the APIs you call require access to encrypted content.
