---
type: Excerpt
canonical_url: https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Guest-to-Guest Workflow In a Nutshell
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide). [Full Markdown](../../../../docs/service-apps-as-g2g-meeting-facilitator-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

In this guide, we will explain how Service Apps in combination with a new subscription can be used to schedule meetings between only guests.



To request or manage this sandbox, open the [official portal page](<https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide>) and sign in.

[Need a Suite Sandbox?](<https://developer.webex.com/docs/developer-sandbox-guide>)

## Selected section

## Guest-to-Guest Workflow In a Nutshell

To develop a guest-to-guest Service App you need to do the following:

1. As a developer, get a trial subscription from `Cisco Commerce Workspace` (CCW) or a [sandbox](https://developer.webex.com/docs/developer-sandbox-guide), which is configured for guest-to-guest meetings. Cisco preconfigures the sandbox with a guest-to-guest meeting site as part of the sandbox setup. You can find the name of the guest-to-guest site by logging in to your sandbox’s Control Hub as an admin and loading the [meeting site list](https://admin.webex.com/meetings/site-list).
1. With your sandbox developer account, log on to [developer.webex.com]() and [create a Service App](https://developer.webex.com/my-apps/new/service-app) with this mandatory and additionally any desired scopes: `guest-meeting:rw`
_Note_: If you want the Service App also to create guests, you must additionally select the scopes - `guest-issuer:write` and `guest-issuer:read` ([see this guide for Service Apps guest creation.)](https://developer.webex.com/docs/sa-guest-management). Generally, you would employ Service App guest creation only in cases where you need to provide some persistence for the guest. For example, if the doctor communicates with the patient over time in a space. We will describe the persistent guest flow later in this document.
1. Submit your app for admin approval. This action makes your Service App visible to an admin in Control Hub in your organization, here an admin for your sandbox.
1. As an admin in [Control Hub](https://admin.webex.com), authorize your Service App to manage your guest-to-guest site and meetings. This can be done in Control Hub [here](https://admin.webex.com/apps/service-apps). Your Service App must be tied to only one available guest-to-guest site. For now, there is a 1 to 1 mapping between a service app with the guest `meeting:rw` scope and a guest meeting site.
_Note_: In the Sandbox Environment, the Service App is licensed for up to 10 simultaneous meetings.
1. As a developer, retrieve the access and refresh tokens for the service app in your Service App details page on developer.webex.com. The tokens should be safely stored. They are used to make the API calls to the Webex developer platform on behalf of the Service Apps machine account which was created in the organization. For a more automated way of being informed about a Service App authorization and subsequent token retrieval, please see [here](https://developer.webex.com/docs/service-apps)
1. With the access token in hand, schedule a meeting via the [meetings API](https://developer.webex.com/meeting/docs/api/v1/meetings/create-a-meeting). The meeting `siteUrl` must be the guest-to-guest site and should be autoconfigured during the Service App licensing and authorization process.
1. Create [join links](https://developer.webex.com/meeting/docs/api/v1/meetings/join-a-meeting) for the guests. When the scheduled time comes around, the guests can use the join link to attend the meeting. You may need to have one guest use the `startLink` while the other guest gets the `attendeeLink`. The guest with the `startLink` will be treated as host.
Your guests, that are not licensed for Webex Meetings can now experience the full meeting experience. 
_Note_: The guest-to-guest meeting is not limited to 2 guests. If desired many guests and also guests and license hosts can meeting in the guest-to-guest Service App scheduled meeting.
