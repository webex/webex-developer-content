---
type: Excerpt
canonical_url: https://developer.webex.com/docs/space-meetings-migration
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Workflow Changes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/space-meetings-migration). [Full Markdown](../../../../docs/space-meetings-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This documentation describes the upcoming changes in meetings workflow functionality for the mobile and web SDKs. It also includes links to detailed migration documentation.



To request or manage this sandbox, open the [official portal page](<https://developer.webex.com/docs/space-meetings-migration>) and sign in.

## Selected section

## Workflow Changes

The following table details the changes in meetings workflow functionality.

#### Legend

<br/>

● = API Change

○ = No API Change

■ = Experience Change

□ = No Experience Change



| **Available API Function**                                                 | **API Caller is from the space-owning org**                     | **API Caller is from an external org**                           | **API Caller is from the free consumer org**                         | **Notes**                                                    |
| ------------------------------------------------------------ | --------------------------------------------------- | ------------------------------------------------------------ | --------------------------------------------------------- | ------------------------------------------------------------ |
| Create a meeting using Public APIs<br /><br /> ● ■<br />     | Space **✓**<br />Instant **✓**<br />Scheduled **✓** | Space **Х**<br />Instant **Х**<br />Scheduled **✓**          | Space **X**<br />Instant **X**<br />Scheduled **✓**       | **Before:** Meeting link is static and retrieved using `roomId`.<br /><br />**After:** Meeting link is dynamic. A developer needs to call the public API to create a meeting link. |
| Start a meeting without waiting in the lobby when`enabledJoinBeforeHost` = `false` (SDK)<br /><br /> ● ■<br /> | Space **✓**<br />Instant **✓**<br />Scheduled **✓** | Space **Х**<br />Instant **✓**<br />Scheduled **X**<br /><br />**NOTE**: In the Webex app, a space meeting also requires the invitee list to be populated. Not everyone becomes a co-host. Non-invitees will be in the lobby. | Space **Х**<br />Instant **✓**<br />Scheduled **X**<br /> | **Before:** Participant can start meetings using the `roomId`.<br /><br />**After:** Participant requires the meeting link, meeting number, or SIP URI to start the meeting.<br /><br />**Space**: A consumer org or external org participant who is **NOT** a member of the space has to be admitted by host even if a password is used to join meeting.<br /><br />**Instant**: Anyone can join an instant meeting before the host without waiting in lobby.<br /><br />**Scheduled**: A consumer org or external org participant does **NOT** have to be admitted by the host when a password is used to join  the meeting. |
| Start a meeting without waiting in the lobby when `enabledJoinBeforeHost` =`true` (SDK)<br /><br /> ● ■<br /><br /> | Space **✓**<br />Instant **✓**<br />Scheduled **✓** | Space **✓**<br />Instant **✓**<br />Scheduled **✓**          | Space **✓**<br />Instant **✓**<br />Scheduled **✓**       | **Before:** Participant can start the meeting using `roomId`.<br /><br />**After:** Participant requires the meeting link, meeting number, or SIP URI to start the meeting. |
| Join after a meeting starts (SDK)<br /><br /> ● ■<br />      | Space **✓**<br />Instant **✓**<br />Scheduled **✓** | Space **✓**<br />Instant **✓**<br />Scheduled **✓**          | Space **✓**<br />Instant **✓**<br />Scheduled **✓**       | **Before:** Participant can start the meeting using `roomId`.<br /><br />**After:** Participant requires the meeting link, meeting number, or SIP URI to start the meeting. |
| Use the host PIN to become the meeting host<br /><br />○ □<br /><br /> | Space **✓**<br />Instant **✓**<br />Scheduled **✓** | Space **✓**<br />Instant **✓**<br />Scheduled **✓**          | Space **✓**<br />Instant **✓**<br />Scheduled **✓**       | 1. A host PIN or password is required only for participants who are **NOT** on the invitee list or **NOT** a member of the space.<br /><br />2. When a participant joins using a meeting number or SIP address they are prompted to enter the host PIN or meeting password. Participants can enter the host PIN and join the meeting as a host.<br /><br />3. When a participant joins using a meeting link they will **NOT** be prompted to enter a PIN or password. Participants can join meetings but will not be hosts.  (Participant can become hosts mid-meeting by using the `reclaim host` API to enter the host      PIN and they can be made hosts by an existing host by calling the `make host` API. |
| Join a meeting after entering a password or captcha<br /><br /> ● ■<br /><br /> | Space **✓**<br />Instant **✓**<br />Scheduled **✓** | Space **✓**<br />Instant **✓**<br />Scheduled **✓**          | Space **✓**<br />Instant **✓**<br />Scheduled **✓**       | **Before:** Participant can start the meeting using `roomId`.<br /><br />**After:** Participant requires the meeting number, or SIP URI to start the meeting. 5 wrong password entries require solving a captcha.<br /><br />1. A password is required only for participants who are **NOT** a part of the invitee list or **NOT** a member of the space.<br /><br />2. When a participant joins using meeting number or a SIP address, they will be prompted to enter host PIN or meeting password. Participants can enter the password and join the meeting as a regular participant. |
| Invite additional participants mid-meeting<br /><br /> ● □<br /> | Space **✓**<br />Instant **✓**<br />Scheduled **✓** | Space **✓**<br />Instant **✓**<br />Scheduled **✓**          | Space **✓**<br />Instant **✓**<br />Scheduled **✓**       | Only the host or co-host can invite additional participants to the meeting. |
| Initialize the Webex Assistant mid-meeting<br /><br /> ○ ■<br /> | Space **✓**<br />Instant **✓**<br />Scheduled **✓** | Space **✓**<br />Instant **✓**<br />Scheduled **✓**          | Space **✓**<br />Instant **✓**<br />Scheduled **✓**       | **Before:** Space meetings do not have advanced meeting capabilities via Webex Assistant such as starting transcriptions, captions, languages, etc.<br /><br />**After:** Space meetings have the same capabilities as regular Webex meetings when the Webex Assistant is enabled.<br /><br />1. Only meetings created by a licensed user can enable the Webex Assistant features. <br /><br />2. Any participant with the host role can start the Webex Assistant.<br /> |
