---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/web-calling-sdk-click-to-call
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Prerequisites
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/web-calling-sdk-click-to-call). [Full Markdown](../../../../../docs/sdks/web-calling-sdk-click-to-call.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Click-to-Call allows users to make calls without the need for a registered account and provides a convenient way for guests to join conversations and participate in audio calls. This article outlines how a click-to-call flow can be set up and utilized using the Web Calling SDK.

---

One of the key use cases is leveraging for **click-to-call** flows, where users can initiate a call by simply clicking a button or link. This is particularly useful in scenarios where the user does not need to manually enter any call details, making the process quick and user-friendly.

## Selected section

## Prerequisites

Before continuing, complete the following steps:

1. The admin needs to enable Click-to-Call in the Webex Control Hub by following the [Click-to-Call Access](https://help.webex.com/article/ndzk21eb/) instructions. This step must be completed before proceeding with any other configurations. Once Click-to-Call is enabled, create a service app. See the following guide for details: [Registering a Service App](https://developer.webex.com/docs/sdks/service-apps).

2. Create a guest using your newly created service app. See the following guide for details: [Creating a Guest Using the Service App](https://developer.webex.com/docs/sa-guest-management).

3. Make an API call to request a `jwe` token. See the following API specification for details: [Generate Guest JWE Token](https://developer.webex.com/calling/docs/api/v1/beta-click-to-call/create-a-call-token).
