---
type: Article
title: New Webex Room Tabs API
canonical_url: https://developer.webex.com/blog/new-webex-room-tabs-api
content_type: blog
date: '2021-07-06'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/new-webex-room-tabs-api)

Room Tabs represent an always available tab that is added to a space, and are configured with a content URL. Just like in the Webex app, you must be a member of the space in order to see its Room Tabs.

### What to use these for?

* **In your team space**: add a tab with your team intranet page.
* **In a finance space**: add a tab with a specific Smartsheet.
* **For an event space**: add tabs for event project management tools.
* **For file access**: add box.com tab to see files or a folder in a space.
* **In brainstorming spaces**: add a Miro tab.
* **In a project space**: add a Trello tab.

The same applies to any other web-based tool.

### Authentication

When a login is required for URLs used in space tabs, you must login. Tools that use Single Sign On will make life easier. Think "do all members of this space have access to the page shown in this tab?".



> **Info**
>
> When you click a tab one more time a menu appears with the following options:



![Room Tabs Menu Options][1]



> **Info**
>
> You can also move the space tab into a separate window by clicking the icon marked here:



![Separate Window Icon][2]

### Room Tab API call

When **viewing** all space tabs using the room tabs API, you can expect something like this:

```json
{
  "items": [
    {
      "id": "Y2lzYGFMDExZWYzOmNkZTGQtMTFlNS1iYTljLTdiNjU1NmQyMjA3Yg",
      "roomId": "Y2lzYGFyJP0JjZWImMS0zYjU4LTkxNDctZjE0YmIwYzRkMTU0",
      "roomType": "group",
      "displayName": "Project Management HomePage",
      "contentUrl": "https://int.cisco.com/projectmanager/233210119",
      "creatorId": "Y2lzY29IzNjE4Ny1jOGRkLTQ3MOGIyZi1mOWM0mMjkwNDY",
      "created": "2021-05-18T26:14:16"
    }
  ]
}
```

Where:

* **id** = the space tab ID
* **roomId** = space that the tab is visible in
* **displayName** = Title of the tab
* **contentUrl** = Tab content source URL
* **creatorId** = userId of the person who added the tab
* **created** = date & time

When creating a space tab, the following items are required:

* roomId
* contentUrl
* displayName

Besides creating room tabs, you can also remove/update/read them.

Be sure to check out the API docs for room-tabs at [https://developer.webex.com/docs/api/v1/room-tabs][3]. We are excited to see what you build!


  [1]: https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt199b17e0ff840d2c/60e466f8e743d53d6a654898/room-tabs-1.png
  [2]: https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt05dd7c9c70c3d46c/60e466f848dce53d63b22ad6/room-tabs-2.png
  [3]: https://developer.webex.com/docs/api/v1/room-tabs
