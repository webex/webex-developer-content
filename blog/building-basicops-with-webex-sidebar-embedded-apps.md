---
type: Article
title: Building BasicOps with Webex Sidebar Embedded Apps
canonical_url: https://developer.webex.com/blog/building-basicops-with-webex-sidebar-embedded-apps
content_type: blog
date: '2023-08-14'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/building-basicops-with-webex-sidebar-embedded-apps)

BasicOps isn’t just a regular Project Management tool, it is “the one place” to work together on projects, tasks, and notes by communicating and messaging with the relevant people in real time.

BasicOps is super easy to use for anyone, not just project managers. Teams can keep conversations about work in “one place” and avoid endless discussions in email and Slack. For team meetings you can collaborate directly in project notes and turn action items into tasks.

### BasicOps and Webex

When Webex first announced the support of Embedded Apps, BasicOps was among the first companies to implement an integration, providing extra value to Webex users. The BasicOps app for Webex Meetings provides an easy way to collaborate on meeting notes, and the BasicOps app for Webex Messaging provides the full functionality of BasicOps, including task management, notes, collaboration, and much more.

### Webex Sidebar Apps

In June, Webex [announced](https://developer.webex.com/blog/webex-sidebar-apps) that the embedded apps framework has been expanded to allow developers to build Sidebar apps. These apps reside on the navigation panel/sidebar of Webex’s application, outside of the meetings and spaces. Developers can also configure these applications to always be running, so that when you launch the Webex App, the applications start up in the background.

When Webex announced the Sidebar Embedded App, we decided that this could provide additional value for our customers, especially for the users who would use BasicOps in multiple spaces. It provides easy access to BasicOps no matter where you are in the Webex app, and it allows BasicOps to inform the user when important information arrives, using the badge feature.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb376bc3db2b5b0dc/64d5189f5252a0466748d74f/image-1.png)

Building an app for the Webex Sidebar is not that hard. If you’re interested, here are some prerequisites to consider and some thoughts about how to get started.

### Responsive Web Design

It is very important that your app supports [Responsive Web Design](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design). If your sidebar app supports the ‘always-on’ feature (more about that later), your app will initially be rendered in a very small hidden window. Then, when the user selects your app, it will become visible and resize to the current size of the Webex app content area. Your app should be able to handle all sizes from mobile phone sizes (or smaller) up to full screen.

### Configuring Your App

If you already have developed a Webex Embedded App for meetings or messaging you just need to update the configuration to support the sidebar as well. If this is your first Webex Embedded App, follow the instructions on [/docs/embedded-apps-guide](https://developer.webex.com/docs/embedded-apps-guide) in the section ‘Creating an Embedded App in the Developer Portal’.

For the sidebar app the following configuration settings are important:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt0c0f1770dcd8b656/64d5189f092e8170e164a374/image-2.png)

Make sure the “Sidebar” option is checked and check the other options only if you’re planning to support them right away (or if you’re already supporting them). If you check the other options without having full support, it may delay the review process, so it may be better to just check the Sidebar option now, and then consider adding the other options later.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb00a19a12d67293a/64d5189f4e6120628dd4d911/image-3.png)

If you’re planning on using the badge or incoming call event features (see below), you need to check ‘Always-on App support’, otherwise those features will not work. If you enable the ‘always-on’ feature, the Webex app will automatically start your app in a small hidden window when the Webex app is started.

### Badging

Showing a notification badge in the sidebar is a great non-intrusive way to let the user know that new information is available without necessarily interrupting what the user is currently doing. In BasicOps, we use this to let the user know that important information is available, such as a new task assigned, a direct message from another user, or a follow-up or mention in a message.

Updating the badge in the Webex sidebar is different from what you may be used to from iPhone and Android phones, where you can use push notifications to update the badge even when the app is not running. In the Webex Sidebar, you have the option to enable the ‘always-on’ feature, which means that your app will be started automatically when the Webex app is started. This makes your app stay active, allowing it to stay connected to your server's backend so it can receive important information in real-time. Your app can then use the Webex Embedded App SDK to set the badge programmatically. You can find an example of setting the badge here: [https://dev.d1pdtdmz00p6qr.amplifyapp.com/interfaces/IWebexAppsSidebar.html#showBadge](https://dev.d1pdtdmz00p6qr.amplifyapp.com/interfaces/IWebexAppsSidebar.html#showBadge)

If you’re having trouble getting the show badge feature to work, you should check the following:

- Make sure you call the Webex SDK functions only after the SDK module is ready. You’ll see an example of how you can do that at [/docs/embedded-apps-framework-sidebar-api-quick-start](https://developer.webex.com/docs/embedded-apps-framework-sidebar-api-quick-start).
- Make sure you configured your app to be ‘always-on’, see ‘Configuring your app’ above.
- Make sure that the installation of your app has also enabled ‘always-on’, see ‘Installing your app’ below.

<br/>

### Incoming Call Events

One of the great features available in the Webex Sidebar Embedded App is that your app can listen for incoming calls to the Webex app. If your app supports Customer Relationship Management type of information, this feature could allow your app to look up a contact immediately when the call is coming in, even before the user responds to the call. This could have your app prepare information about the incoming call and inform the user about the caller.

In BasicOps we currently do not have this type of information, so we have not implemented this part, but if your app supports this type of information I recommend that you check out the sample implementation here: [/docs/embedded-apps-framework-sidebar-api-quick-start](https://developer.webex.com/docs/embedded-apps-framework-sidebar-api-quick-start)

### Installing Your App

The process of installing the sidebar app is different from the other types of embedded apps, where each individual user can select from a list of apps. The sidebar app can be installed only by the Webex administrator.

The Webex administrator can enable the sidebar app by selecting Apps in the Management section in the sidebar, then selecting the Embedded Apps tab. During this phase of development, your app will probably be in the “Private” section, and you may need to enable ‘Show In-development apps’.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte600897cb1218d3d/64d5189f2f9b606e7c305f50/image-4.png)

Once the administrator has located your app, the administrator can select which users should have access to the app. On that same page, the administrator needs to locate the ‘Sidebar settings’ and enable ‘Show app in sidebar’. If your app is using the ‘always-on’ feature, the administrator will also see an option to enable that: ‘Make always on’. It’s very important this is checked as well, otherwise the badge and incoming call events features will not work.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbab533eb8f9e0aa3/64d5189fabde6ac2b451e046/image-5.png)

If you can’t get your Webex administrator to install your app, you should consider requesting a developer sandbox from Webex. With that, you’ll get full administrator privileges, so you’ll be able to install and test your app in the sandbox. To request a developer sandbox, go to [/docs/developer-sandbox-guide](https://developer.webex.com/docs/developer-sandbox-guide).

### If this is your first Webex Embedded App...

You can find a great guide for creating your first Webex Embedded App here: [/docs/embedded-apps-guide](https://developer.webex.com/docs/embedded-apps-guide). However, this is using version 1 of the SDK, while you must use version 2 to get full support for the sidebar functions. So when you get to the JavaScript part of your app, you should consult [/docs/embedded-apps-framework-sidebar-api-quick-start](https://developer.webex.com/docs/embedded-apps-framework-sidebar-api-quick-start) (quick start guide for sidebar apps) and [https://dev.d1pdtdmz00p6qr.amplifyapp.com/classes/Application.html](https://dev.d1pdtdmz00p6qr.amplifyapp.com/classes/Application.html) (SDK version 2 reference).

### If you already have a Webex Embedded App...

If you’ve already implemented a Webex Embedded App for meetings or for messaging, you should make sure that you’re using the latest version of the Webex JavaScript library. You may be using version 1, but you’ll need to use version 2 to get full support for the sidebar functions. If you need to upgrade, you can find a guide here: [https://dev.d1pdtdmz00p6qr.amplifyapp.com/index.html#migration-from-1x-to-2x](https://dev.d1pdtdmz00p6qr.amplifyapp.com/index.html#migration-from-1x-to-2x)

### Conclusion

If you already have a well-functioning app using Responsive Web Design and it makes sense to include it in the Webex sidebar, it is a fairly simple process to make that happen. Implementing the features you want to support in the sidebar app is probably simpler than if you decide to support the meeting and space apps as well.

Webex has great documentation helping you through the process, but beware that some of the documentation refers to SDK version 1, while you need version 2. If you still run into issues, you can’t quite figure out, I can tell you from personal experience that Webex has an excellent support team.

Once you’re ready to publish your app to the world via the Webex App Hub, you will do that from the developer portal. From my experience, once you submit your app you’ll get feedback from the Webex reviewers quickly - or your app will be approved to be present on the Webex App Hub!

Good luck with your next app!
