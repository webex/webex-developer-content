---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Messaging Policy Behavior
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel). [Full Markdown](../../../../docs/bring-your-own-custom-messaging-channel.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md) [Authentication For Custom Messaging Integrations](004-authentication-for-custom-messaging-integrations.md) [Attachment URL Requirements](011-attachment-url-requirements.md)

## Article introduction

Connect an external messaging channel to Webex Contact Center through middleware that uses the Custom Messaging APIs.

## Selected section

## Messaging Policy Behavior

Messaging policies are configured on the Custom Messaging channel in Control Hub under Contact Center > Channels & Assets > Channels > Custom Messaging. These policies control:

- Maximum message characters
- Whether attachments are allowed
- Maximum number of attachments
- Maximum total attachment size
- Maximum single attachment size
- Allowed file types

If an inbound message violates the configured channel policy, the entire message is rejected rather than partially accepted.

If administrators update the messaging policy, inbound middleware traffic starts using the updated policy almost immediately after the configuration change is applied. For outbound agent messaging, the updated policy is applied after the next relevant desktop reload or session refresh.
