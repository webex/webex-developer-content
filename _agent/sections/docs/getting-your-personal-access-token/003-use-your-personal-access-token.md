---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-your-personal-access-token
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
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
