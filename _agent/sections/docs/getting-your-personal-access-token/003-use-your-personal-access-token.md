---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-your-personal-access-token
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Use your personal access token
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/getting-your-personal-access-token). [Full Markdown](../../../../docs/getting-your-personal-access-token.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Learn how to get a personal access token for testing Webex APIs with your own account.

## Selected section

## Use your personal access token

You use your personal access token like any API access token, for example:

```bash
$ curl --request GET \
  --header "Authorization: Bearer <YOUR_PERSON_ACCESS_TOKEN>" \
  https://webexapis.com/v1/rooms/
```
