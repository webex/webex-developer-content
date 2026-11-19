---
type: Excerpt
canonical_url: https://developer.webex.com/docs/introduction-to-webex-apps
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- About Webex Extensibility
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/introduction-to-webex-apps). [Full Markdown](../../../../docs/introduction-to-webex-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This tutorial provides an introduction to Webex's extensibility.

---

In this introduction to the Webex REST API, you will use the interactive documentation to experience Webex programmability. The tutorial will then go through a few use-cases, and drill into the fundamentals of Webex Apps.

## Selected section

## About Webex Extensibility



> **Info**
>
> *NOTE*: Webex *rooms* were renamed *Spaces*. However, the REST API still uses the `/rooms` resource, and you may see the 'Space' and 'Room' terms used interchangeably.



Extending Webex enables you to create applications that:

- Automate tasks such as creating spaces, posting messages, or adding participants to an existing space.
- Perform actions in response to events in Webex such as participants being added to spaces, or new messages being created.

To automate tasks, custom applications use the [Webex REST API](https://developer.webex.com/docs/api/getting-started).

The API enables you to interact with Webex's main concepts:

- [Rooms](https://developer.webex.com/docs/api/v1/rooms): Create, update or delete spaces.
- [Teams](https://developer.webex.com/docs/api/v1/teams): Create, update or delete teams.
- [People](https://developer.webex.com/docs/api/v1/people): Look for Webex users.
- [Messages](https://developer.webex.com/docs/api/v1/messages): Create or delete Messages.
- [Memberships](https://developer.webex.com/docs/api/v1/memberships) and [Team Memberships](https://developer.webex.com/docs/api/v1/team-memberships): Add, remove participants from spaces and teams, and promote participants as moderators.

Moreover, your application can register [Webhooks](https://developer.webex.com/docs/api/v1/webhooks) to be notified of various events, such as new messages being posted, or users joining or leaving spaces.

The documentation listed above enables you to interact with the Webex API straight from your Web browser. Because you will use the interactive documentation throughout these tutorials, you will start by exploring it here. Moreover, doing so will help demonstrate these extensibility concepts!*
