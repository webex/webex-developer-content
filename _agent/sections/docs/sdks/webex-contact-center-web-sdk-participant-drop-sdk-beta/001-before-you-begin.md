---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-participant-drop-sdk-beta
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-participant-drop-sdk-beta). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-participant-drop-sdk-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Participant Drop lets the primary agent remove an eligible participant from an active Webex Contact Center voice conference. Use the voice task's `dropConferenceParticipant` method, then refresh your application from the updated task rather than removing a participant from the UI immediately.

## Selected section

## Before you begin

- Complete the [Web SDK Quickstart](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart) and [Authentication guide](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication). Register each test agent, complete station login, and confirm that they can receive voice tasks.
- Use an approved beta SDK build and a Webex Contact Center organization where the routing service supports Participant Drop. There is no client-side SDK feature flag; the service decides whether a request is authorized.
- Prepare a test customer and at least three test agents so you can check conference, ownership-change, and consult scenarios without using real customer data.
