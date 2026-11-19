---
type: Excerpt
canonical_url: https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Overview of Guest-to-Guest Meetings
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide). [Full Markdown](../../../../docs/service-apps-as-g2g-meeting-facilitator-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

In this guide, we will explain how Service Apps in combination with a new subscription can be used to schedule meetings between only guests.



To request or manage this sandbox, open the [official portal page](<https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide>) and sign in.

[Need a Suite Sandbox?](<https://developer.webex.com/docs/developer-sandbox-guide>)

## Selected section

## Overview of Guest-to-Guest Meetings

In the context of guest-to-guest Webex meetings, guests are defined as non-licensed users. Guests are often used in applications that provide some form of expert services. For example, a doctor may talk to a patient or a customer to a support agent, or a plumber may have a video conference with a homeowner to pre-consult the work. Common to these use-cases, is the idea that none of the participating parties are permanently licensed as hosts for Webex meetings.

In the past, these apps were built on top of space-backed meetings where a space was established between the two parties to conduct the meeting. This approach used to work, albeit with limited functionality. For example, recording the meeting, providing meeting transcripts, or patching in a translator was impossible. In addition, meetings between guests only are expressly denied under our terms and conditions, which in all cases need a licensed user to sponsor the meeting.

With the advent of the Webex Suite Meeting Platform (WSMP) the approach to guest-to-guest meetings is changing. The space-backed meetings are no longer available and instead replaced by regular Webex Meetings licensed by a guest-to-guest Service App. The proven and successful meeting’s backend now powers all meeting functionality. The new attendee experience is a full-featured meeting with all the standard meeting controls like recording, transcription, etc., available even when only guests participate. The meetings infrastructure licenses the guest-to-guest meeting experience from the licensed Service App, which only counts the number of simultaneous meetings. The following sections provide additional background information and developer guidance on the development of guest-to-guest Service Apps.
