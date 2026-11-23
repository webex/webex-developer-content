---
type: Excerpt
canonical_url: https://developer.webex.com/docs/browser-sdk-messaging-tutorial
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Getting your Personal Access Token
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/browser-sdk-messaging-tutorial). [Full Markdown](../../../../docs/browser-sdk-messaging-tutorial.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

## Getting your Personal Access Token

Webex REST API calls require an API access token in the request header. For real-world
applications you want to obtain an access token from a user using a [Webex Integration](https://developer.webex.com/docs/integrations) and OAuth. For testing purposes however you can use your personal access token available in the Developer Portal.

The Webex JS SDK's `init()` takes a JSON object that determines how it will authorize API requests

**To use your personal access token**:

1. Copy your access token from the form below (you must be [signed in](https://developer.webex.com/login) to the Developer Portal).

    

To view or copy your personal access token, open the [official portal page](<https://developer.webex.com/docs/browser-sdk-messaging-tutorial>) and sign in.



2. Open index.js and paste your access token for the value of `access_token`:

    ```javascript
    const webex = (window.webex = window.Webex.init({
        credentials: {
            access_token:
            "<YOUR-ACCESS-TOKEN-HERE>",
        },
    }));
    ```

3. Save your changes to index.js.
