---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-your-own-onenote-bot-integrated-with-webex
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Additional Resources
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-your-own-onenote-bot-integrated-with-webex). [Full Markdown](../../../../docs/create-your-own-onenote-bot-integrated-with-webex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article explains how you can create your own Webex-integrated OneNote bot.

## Selected section

## Additional Resources

For more information on OneNote and Webex, see:

- **OneNote API Documentation**: [https://learn.microsoft.com/en-us/graph/api/resources/onenote-api-overview?view=graph-rest-1.0](https://learn.microsoft.com/en-us/graph/api/resources/onenote-api-overview?view=graph-rest-1.0)
  Please note that OneNote does not support a webhook-based notification mechanism. Instead, it requires periodic polling of the OneNote APIs to detect any changes. For example, to be informed when a new notebook is created, the ‘[List notebooks](https://learn.microsoft.com/en-us/graph/api/onenote-list-notebooks?view=graph-rest-1.0&amp;tabs=http)' API must be invoked at regular intervals, such as every five minutes and the response compared with the previously retrieved list to identify any differences and trigger notifications accordingly.
- **Webex API Documentation**: [https://developer.webex.com/docs](https://developer.webex.com/docs).
