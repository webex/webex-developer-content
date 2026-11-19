---
type: Article
title: Introducing the Webex Messaging Announcement Mode API
canonical_url: https://developer.webex.com/blog/introducing-the-webex-messaging-announcement-mode-api
content_type: blog
date: '2021-12-10'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/introducing-the-webex-messaging-announcement-mode-api)

[Announcement mode in Webex messaging](https://help.webex.com/en-US/article/n0wbhrz/Webex-App-%7C-Send-announcements-in-moderated-spaces) allow bots and integrations to share important information inside a Webex space, without the distractions from other conversations. For example, announcement spaces are a great way to send automated alerts and notifications that won’t get buried by other messages. From there, it can perhaps guide to users to the appropriate conversation spaces to follow up on the notifications.

These type of announcement spaces can now be created by Webex bots and integrations in one step, allowing a streamlined approach for developers to enable this functionality in their apps. This new API method also allows the quicker creation of moderated spaces, so there is much to like!

### How an App Creates a Webex Space in Announcement Mode

Bots and integrations can create a Webex messaging space in announcement mode with some new parameters that have been added to the [rooms API](https://developer.webex.com/docs/api/v1/rooms/create-a-room): `isLocked` and `isAnnouncementOnly`.

- First, since a Webex space is required to be locked to enable announcement-mode, the value for `isLocked` must be set to true. This will tell Webex to create a locked space, with the authenticated user/bot assigned as the default moderator.
- Next, by also setting the `isAnnouncementOnly` value to true, the locked space will be created in announcement mode, where only the assigned moderators can post messages.

Using those two parameters, the API request to create an announcement space named “ALERTS” might look something like this:

```bash
https://webexapis.com/v1/rooms -H "Content-type: application/json" -d '{"title":"ALERTS","isLocked":true,"isAnnouncementOnly":true}'
```

### More Webex Announcement Space Tidbits

As you see, the APIs for creating a Webex space in announcement-mode is rather straightforward. However, there are a few other things to keep in mind when leveraging this in an application:

- The ability to create a locked Webex messaging space or act as moderator is **not** available in accounts under the [Cisco Webex Free Plan](https://help.webex.com/en-US/article/n19jg1u/Cisco-Webex-Free-Plan-Features#id_133759), from either the Webex app or the corresponding APIs.
- Bots and integrations can add or update the moderators in announcement spaces just like traditional group messaging spaces - through the `isModerator`parameter in the [Memberships API](https://developer.webex.com/docs/api/v1/memberships). Prior to this update, this was the only way to even create a locked Webex space.
- Announcement spaces can always be quickly changed back to a group space and keep the moderators by simply [updating](https://developer.webex.com/docs/api/v1/rooms/update-a-room) the /room `isAnnouncementOnly` parameter to *false*.

As always, you can count on the awesome [Webex Developer Support](https://developer.webex.com/support) team to assist with any questions or challenges that come up. In the meantime, happy developing!
