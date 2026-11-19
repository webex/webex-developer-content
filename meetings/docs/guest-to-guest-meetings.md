---
type: Guide
title: Guest to Guest Overview
display_title: Guest to Guest Overview
canonical_url: https://developer.webex.com/docs/guest-to-guest-meetings
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/guest-to-guest-meetings)

Guest-to-Guest meetings in Webex provide a seamless way for non-licensed, anonymous users to host and join flexible, on-demand meetings without requiring permanent licenses or registered identities. This feature is integrated into the Webex Meetings app and managed via a dedicated service app that sponsors these meetings, making it ideal for ad-hoc or one-time gatherings.

---

# Overview of Guest-to-Guest Meetings

In the context of guest-to-guest Webex meetings, guests are defined as non-licensed users. Guests are often used in applications that provide some form of expert services. For example, a doctor may talk to a patient or a customer to a support agent, or a plumber may have a video conference with a homeowner to pre-consult the work. Common to these use-cases, is the idea that none of the participating parties are permanently licensed as hosts for Webex meetings.

In the past, these apps were built on top of space-backed meetings where a space was established between the two parties to conduct the meeting. This approach used to work, albeit with limited functionality. For example, recording the meeting, providing meeting transcripts, or patching in a translator was impossible. In addition, meetings between guests only are expressly denied under our terms and conditions, which in all cases need a licensed user to sponsor the meeting.

With the advent of the Webex Suite Meeting Platform (WSMP) the approach to guest-to-guest meetings is changing. The space-backed meetings are no longer available and instead replaced by regular Webex Meetings licensed by a guest-to-guest Service App. The proven and successful meeting’s backend now powers all meeting functionality. The new attendee experience is a full-featured meeting with all the standard meeting controls like recording, transcription, etc., available even when only guests participate. The meetings infrastructure licenses the guest-to-guest meeting experience from the licensed Service App, which only counts the number of simultaneous meetings.
