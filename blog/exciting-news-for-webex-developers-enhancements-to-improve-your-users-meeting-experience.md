---
type: Article
title: 'Exciting News for Webex Developers: Enhancements to Improve Your Users'' Meeting Experience!'
canonical_url: https://developer.webex.com/blog/exciting-news-for-webex-developers-enhancements-to-improve-your-users-meeting-experience
content_type: blog
date: '2023-08-10'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/exciting-news-for-webex-developers-enhancements-to-improve-your-users-meeting-experience)

Over the next few months, all Webex meetings will start to run on our Webex Suite meeting platform. This platform allows for improved and simplified experiences for hybrid work across the entire Webex Suite, with a common architecture, administration, and integrations. To learn more about these changes, you can refer to [this informative help article](https://help.webex.com/en-us/article/m61d8eb/Webex-App-%7C-About-the-Video-Mesh-ready-meeting-platform#reference-template_f7d2230b-bb3f-4d88-b7b5-d012273b4e4c).

### Changes to Hosting and Joining Meetings

As we move forward, the way meetings are hosted and joined on the Webex Suite Meeting platform will change. In the meantime, we have taken steps to ensure your apps will continue to function as the Webex Suite meeting platform is rolled-out to all Webex sites. If you are currently using our SDKs or Widgets to host or join meetings in a Webex Messaging space in your app, you just need to make a slight workflow adjustment to prepare for this change.

In the past, hosting a meeting in a space was as simple as using the [room ID](https://developer.webex.com/docs/api/v1/rooms/list-rooms) in the join request and the meeting would be automatically generated. However, with the transition to these Webex Suite platform meetings, a [meeting ID](https://developer.webex.com/docs/api/v1/meetings/list-meetings) will be required to join. To create a meeting, you can utilize the "[Create Meeting API](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting)" to set up a meeting before joining. Moreover, it's possible to associate a Webex Meeting with a Webex Messaging space by providing the "roomId" to the "[create meeting](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting)" API, making the process even more seamless for your team.

The good news is that our Webex SDKs and Webex Widgets already fully support joining these Webex Suite platform meetings, ensuring that your users will continue to enjoy the complete Webex Meetings experience. We do recommend getting ahead of this by updating your apps now to take advantage of the new experience when it becomes available.

### Changes for Meetings Attended Only by Guests

One of the significant changes for the Webex Suite platform meetings is that the meetings will need an official "host." This change will impact a small number of developers who have only guests attending their meetings (created with a [guest issuer](https://developer.webex.com/docs/guest-issuer)). Since  Webex Suite platform meetings require a host, and guests currently cannot be hosts, there will be some workflow adjustments. If you do have apps that include guest-only meeting scenarios, please contact our [Developer Support team](https://developer.webex.com/support) for further assistance. We also recommend, to start, getting familiarized with a new application type we now offer, called [Webex Service Apps](https://developer.webex.com/docs/service-apps). This will be the exclusive path for guest-only Webex Meeting integrations in the future.

### Action Required

If you have been hosting meetings in a Webex Messaging space using SDKs or Widgets, please refer to the "Changes to Hosting and Joining Meetings" section above for steps on how to transition to support the Webex Suite platform meetings. Again, for those who have apps with guest-only meeting scenarios (guest host and attendees), please contact our [Developer Support team](https://developer.webex.com/support) for further assistance.

### Timing

The timing of these changes will align with the upgrades to the new Webex Suite meeting platform. Be sure to monitor the "[Webex App | What’s New](https://help.webex.com/en-us/article/8dmbcr/Webex-App-%7C-What%27s-New#Cisco_Reference.dita_0ef76123-0d49-4e62-b537-653ecaa92c98)" article for the specific dates that align with your site’s specific upgrade channel.

### Developer Support

If you have any questions or concerns, our developer support team is always ready to help! Reach out to us at [support](https://developer.webex.com/support).

### Enjoy an Even Better Webex Experience!

We're thrilled about the new Webex Suite platform meetings that will provide your users with an even better Webex experience. Thank you for being a part of the Webex Developers community!
