---
type: Excerpt
canonical_url: https://developer.webex.com/docs/frequently-asked-questions
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Administrative
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/frequently-asked-questions). [Full Markdown](../../../../docs/frequently-asked-questions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

If you don't find the answer you're looking for here, please contact Webex Developer Support.

## Selected section

## Administrative

### How do I revoke an authorization for an Integration?

Org admins can revoke access tokens for users in their org using the [Authorizations API](https://developer.webex.com/docs/api/v1/authorizations).

### I poll the /people API for user status. Why are some of my Org's users not returning any "status" information?

If a user's "status" is returned as "unknown" and the user is a member of your org then that means that they have been inactive for more than 30 days.

### As a Full Admin of my Org, am I able to schedule Meetings and get Recordings for other users within my Org?

Yes. Details can be found on /docs/meetings#adminorganization-level-authentication-and-scopes. Details for what a Compliance Officer can do with the meetings-related APIs can be found on /docs/meetings#compliance-officer-level-authentication-and-scopes.

### As a Compliance Officer, how can I obtain a list of all Teams/Rooms within my Org?

At this time there is no way to list all teams in an org. The work-around is for a compliance officer to pull data from the [/events API](https://developer.webex.com/docs/api/v1/events) to get roomIds, and then GET details of the space using the [/rooms/<roomId> API](https://developer.webex.com/docs/api/v1/rooms/get-room-details) to see if it's part of a team and get the teamId. Once you have the teamIds then you can pull details for the teams and list the team memberships. Note there are upcoming improvements that will allow the compliance officer to directly list all teams and spaces in an org, but there is no ETA for when these will be available.
