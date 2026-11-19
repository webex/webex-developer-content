---
type: Excerpt
canonical_url: https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Meetings without a host role joining
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide). [Full Markdown](../../../../docs/service-apps-as-g2g-meeting-facilitator-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

In this guide, we will explain how Service Apps in combination with a new subscription can be used to schedule meetings between only guests.



To request or manage this sandbox, open the [official portal page](<https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide>) and sign in.

[Need a Suite Sandbox?](<https://developer.webex.com/docs/developer-sandbox-guide>)

## Selected section

## Meetings without a host role joining
Sometimes, it may be desirable not to privilege an attendee with the host role. Instead, both parties will use the attendeeLink to join and start the meeting. To achieve this behavior, you need to do the following:

i. In Control Hub make sure you have enabled the setting “They can join the meeting” under Services -> Meeting -> [Select your guest site] -> All -> Security -> Webex Meeting Security. This allows an attendee to join a meeting without the host.
ii. The Service App [meetingPreferences](https://developer.webex.com/meeting/docs/api/v1/meeting-preferences/get-meeting-preference-details) should include the following settings:

```json
schedulingOptions": {"enabledJoinBeforeHost": true,"joinBeforeHostMinutes": 5,"enabledAutoShareRecording": false,"enabledWebexAssistantByDefault": false},
```

You can retrieve the Service App meetingPreferences using the Service App access Token.
In addition, please make sure that in Control Hub you have enabled the setting “They can join the meeting” under Services->Meeting->[Select your guest site]->All->Security->Webex Meeting Security
iii. When scheduling the meeting via the create a meeting with the Service App access token, please set the following field `"unlockedMeetingJoinSecurity" : "allowJoin”`

### Persistent guests

If you give your Service App the `guest-issuer:read` and `guest-issuer:write` scope, you can use it to create two or more guests. You can do this with a `POST` to `/guests/token` and the `Service App’s` access token as the Bearer token. Details can be found [here](https://developer.webex.com/docs/sa-guest-management). You would then, launch the [SDK](https://developer.webex.com/docs/SDKs/android) with the guest token and let them join the meeting.

The persistent guest approach is also suitable if you want the guests to chat outside a meeting in the Webex App or to reach parity with previous space-backed workflows.

Here is a comparison with the previous workflow:



| Space-backed meeting | Service App guest-to-guest meeting | 
| ---------------- | ------------------- |
| 2 guests are created via guest-issuer app type | Service App creates 2 guests |
| Bot creates a space | Service App creates a space |
| Bot adds 2 people to space | Service App adds two people to space |
| Guests join space and meet (adhoc) | Service App schedules meeting in space and guests can meet* |

Adhoc meetings in spaces can be facilitated by setting the `roomId` and `adHoc=true` in the [create a meeting API call](https://developer.webex.com/meeting/docs/api/v1/meetings/create-a-meeting).
