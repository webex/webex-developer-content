---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhook-event-reference
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Messaging
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webhook-event-reference). [Full Markdown](../../../../docs/webhook-event-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Find Webex Webhooks API resources, events, triggers, filters, and links to product-specific payload definitions.

## Selected section

## Messaging

For bots in group spaces, `messages` notifications are delivered only for messages that mention the bot. See [Differences between bots and people](https://developer.webex.com/docs/bots#differences-between-bots-and-people).

| Resource | Event | Trigger | Supported filters |
| --- | --- | --- | --- |
| `attachmentActions` | `created` | A user interacted with one of your [cards](https://developer.webex.com/docs/buttons-and-cards). | `messageId` — limit to a particular message, by ID.<br />`personId` — limit to a particular person, by ID.<br />`roomId` — limit to a particular room, by ID. |
| `memberships` | `created` | Someone joined a room that you're in or you've been added to a new room. | `roomId` — limit to a particular room, by ID.<br />`personId` — limit to a particular person, by ID.<br />`personEmail` — limit to a particular person, by email.<br />`isModerator` — limit to moderators of a room. |
| `memberships` | `updated` | Someone's membership was updated in a room that you're in; primarily used to detect moderator changes. | `roomId` — limit to a particular room, by ID.<br />`personId` — limit to a particular person, by ID.<br />`personEmail` — limit to a particular person, by email.<br />`isModerator` — limit to moderators of a room. |
| `memberships` | `deleted` | Someone left or was kicked out of a room that you're in, or you left or were removed from a room; only triggers for group rooms, not 1-to-1 rooms. | `roomId` — limit to a particular room, by ID.<br />`personId` — limit to a particular person, by ID.<br />`personEmail` — limit to a particular person, by email.<br />`isModerator` — limit to moderators of a room. |
| `messages` | `created` | New message posted into a room that you're in. | `roomId` — limit to a particular room, by ID.<br />`roomType` — limit to a particular room type (such as `direct` or `group`).<br />`personId` — limit to a particular person, by ID.<br />`personEmail` — limit to a particular person, by email.<br />`mentionedPeople` — limit to messages which contain these mentioned people, by person ID; accepts `me` as a shorthand for your own person ID; separate multiple values with commas.<br />`hasFiles` — limit to messages which contain file content attachments.<br />`hasAttachments` — limit to messages which contain content attachments. |
| `messages` | `deleted` | A message was deleted from a room that you're in. | `roomId` — limit to a particular room, by room ID.<br />`roomType` — limit to a particular room type (such as `direct` or `group`).<br />`personId` — limit to a particular person, by ID.<br />`personEmail` — limit to a particular person, by email.<br />`mentionedPeople` — limit to messages which contain these mentioned people, by person ID; accepts `me` as a shorthand for your own person ID; separate multiple values with commas.<br />`hasFiles` — limit to messages which contain file content attachments.<br />`hasAttachments` — limit to messages which contain content attachments. |
| `rooms` | `created` | A new room was created by you or one of your integrations. | `type` — limit to a particular room type (such as `direct` or `group`).<br />`isLocked` — limit to rooms that are locked. |
| `rooms` | `updated` | A room that you're in was updated; primarily used to detect when a room becomes Locked or Unlocked. | `type` — limit to a particular room type (such as `direct` or `group`).<br />`isLocked` — limit to rooms that are locked. |
| `rooms` | `migrated` | A room you or your bot is in was migrated to a different geography, usually during an organization’s change of data residency. There will be a change in the roomId and your app should use the new roomId. | |
