---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-started
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Accounts and Authentication
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/getting-started). [Full Markdown](../../../../docs/getting-started.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex APIs give you easy access to the Webex Platform to build [Bots](https://developer.webex.com/docs/bots) or [Integrations](https://developer.webex.com/docs/integrations). If you're ready to start using the Webex APIs, keep reading.



To view or copy your personal access token, open the [official portal page](<https://developer.webex.com/docs/getting-started>) and sign in.

## Selected section

## Accounts and Authentication

To use the Webex REST API you'll need a Webex account backed by Cisco Webex Common Identity (CI). If you already have a Webex account, you're all set. If you're using Webex Meetings, your site will [need to be on Common Identity](https://help.webex.com/WBX000023841/).

If you don't already have a Webex account, go ahead and [sign up](https://www.webex.com/pricing/free-trial.html)! You'll need an account to use the APIs and SDKs.

When making requests to the Webex REST API, an `Authorization` HTTP header is used to identify the requesting user. This header must include an access token. This access token may be a [personal access token](https://developer.webex.com/docs/getting-your-personal-access-token), a [Bot](https://developer.webex.com/docs/bots) token, or an OAuth token from an [Integration](https://developer.webex.com/docs/integrations).
