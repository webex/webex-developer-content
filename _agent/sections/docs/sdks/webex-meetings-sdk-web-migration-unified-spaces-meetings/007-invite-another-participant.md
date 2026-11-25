---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Invite another participant
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Limitations](011-limitations.md)

## Article introduction

This guide provides an overview of the improved meeting experience associated with spaces and outlines the impacted areas, along with the necessary adjustments in these areas for the adoption of these improved flows. 

## Selected section

## Invite another participant

A participant can be invited to the meeting using the [invite](https://webex.github.io/webex-js-sdk/api/#meetinginvite) method within the meeting object. Only a host can invite another participant. Participants can be invited using an email address.

Use the following code to invite another participant to an existing meeting. You can use either the `emailAddress` or the `phoneNumber` parameter.

```javascript
meeting.invite(invitee: {
  emailAddress: 'johndoe@abc.com',
  phoneNumber: '1234',
});
```

To cancel an outgoing phone invite, use the following method.

```javascript
meeting.cancelPhoneInvite(invitee: {
  phoneNumber: '1234',
});
```
