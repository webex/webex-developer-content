---
type: Article
title: 'Webex Embedded Apps: New Layout Preference Option'
canonical_url: https://developer.webex.com/blog/webex-embedded-apps-new-layout-preference-option
content_type: blog
date: '2022-06-30'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-embedded-apps-new-layout-preference-option)

If you [created a Webex Embedded App for Meetings](https://developer.webex.com/my-apps/new/embedded-app) in your developer account recently, you may have noticed an update that added a new section for “Layout preference”. This is where you can specify how your embedded app appears for all users (initiator and participants) when the app is launched within a meeting (“[Open for all](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings#recommended-design-guidelines)”).

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc3193d0df3f0cc24/62bdc932f96bd850756d3dfd/ea-layout-pref-blog-1.png)

Before this update, in-meeting embedded apps were launched in a compact “Side Panel” layout, which was not optimal in many cases. With this update, developers can select the new “Main View” preference for the default layout, where the embedded app is launched in a full display like a screen share. This wider view can present a better user experience for apps that utilize more complex arrangements, such as toolbars or other components that a compact view will not allow.

The Webex Embedded App for [Miro](https://apphub.webex.com/applications/miro-miro-18615) is already taking advantage of Main View:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta65c18e9da58635a/62bdc93225ccfe5195056f9c/ea-layout-pref-blog-2.png)

There are some things to keep in mind when selecting between “Side Panel” and “Main View” layout preferences. First, as it is indeed a preference, it may not necessarily be respected in all cases. For example, if the [meeting stage](https://help.webex.com/en-us/article/4tyard/Move-participants-to-the-stage-in-Webex-Meetings,-Webex-Webinars,-and-Webex-Events-(classic)) is currently used by a participant screen share, the embedded app would instead default to a side panel layout when launched. This preference also only applies to the in-meeting experience and does not include embedded apps on Webex messaging spaces. Additionally, as embedded apps start becoming available for [Webex devices](https://blog.webex.com/hybrid-work/favorite-business-apps-on-webex-devices/), the “Main View” will be required as the default layout.

As you can see, implementing the new “Main View” layout preference is rather straightforward and enables more UI/UX design options for Webex Embedded Apps. Of course, if you have questions or any need assistance with creating an embedded app in Webex, our [developer support team](https://developer.webex.com/support) is always happy to help.
