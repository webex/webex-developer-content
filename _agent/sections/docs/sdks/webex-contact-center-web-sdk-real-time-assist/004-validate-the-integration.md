---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-real-time-assist
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Validate the integration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-real-time-assist). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-real-time-assist.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test Real Time Assist with the Webex Contact Center SDK. Start with the sample application, then add the request, response, and feedback handling to your application.

## Selected section

## Validate the integration

Complete an active voice interaction and verify that:

- A request without extra context completes without an SDK error.
- The task receives a `SUGGESTED_RESPONSE` event and your application displays the response.
- A request with extra context returns a new response for the same interaction.
- Like, dislike, and copy actions complete without an SDK error and use the correct `adaptiveCardId`.
- Ending an interaction clears its responses from your UI, and a new interaction does not show content from the previous customer.
