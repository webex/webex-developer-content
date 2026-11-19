---
type: Article
title: The New Webex Meetings Widget
canonical_url: https://developer.webex.com/blog/the-new-webex-meetings-widget
content_type: blog
date: '2022-01-13'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/the-new-webex-meetings-widget)

[Webex Widgets](https://developer.webex.com/docs/widgets) provide developers with the ability to include Webex native applications features directly into their web applications with just few lines of code. It is beneficial for use cases where faster integrations are needed where developers don’t want to worry about the user interface or user experience. We are excited to announce the release of the new [Webex Meetings Widget](https://developer.webex.com/docs/widgets#meetings-widget-). The Meetings Widget provide the developers with the ability to embed Webex meetings functionality into their web-based applications. 

![Meetings Widgets][1]

### Why Webex Meetings Widget?

Webex Meetings Widgets provide extensive flexibility...

#### Join Any Webex Meeting Type!

Join the particular type of Webex Meeting that satisfies your use case! The new widget provides the ability to join Webex meetings regardless of the meeting type. Using this widget, users can join any of the following meetings as: Space (1:1/group), Scheduled meetings, Personal meeting rooms and even call a cloud registered Webex device!

#### Different layouts 

When initializing the widget, you will be able to set the video layout. We currently support the following layouts on the widget:

- Grid
- Focus
- Prominent
- Overlay
- Stack

&nbsp;
&nbsp;

#### Responsive Design!

If your web application runs on mobile, tablet, and desktop browsers and you don't want to build a dedicated mobile application to join Webex meetings, then this widget is right for you. It was designed to be responsive which means not only a fast integration, but also the ability to adapt to your screen size on  Desktop, Tablet, and Mobile for better user experience

![Widget-mobile](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb128d4008f79a6be/61ddad121757dc6aed2ae142/Mobile.png)

#### Customization

Let us assume that you want your end users to use the widget to join a meeting, but at the same time you want to prevent the user from using screen sharing. The widget comes with ability to customize the controls, so that you can show/hide these controls based on your use case! Also, the widget comes with 2 themes, a dark and a light one.

#### Accessibility

Here in Webex, we think about all our users. The widget provides the following accessibility features:

- Screen reader – We have labeled the different components on the widget for the browser screen readers to be able to read these labels to visually impaired users
- Keyboard tabbing – You can use the keyboard to tab through the different widget controllers and settings

&nbsp;
&nbsp;

#### Media Devices Management & Screen Sharing

The widget provides users with the ability to select their media devices pre-meeting as well as mid-meeting, and lets you mute/unmute both your Microphone and Camera. Users will also be able to share their screens as well as view the shared screens of other participants. Please note that screen sharing is not supported on Mobile browsers due to OS limitations

### Getting Started

We have written a quick start application that will allow you to get up and running with the new Meetings widget in no time! The setup is a basic site that utilizes the implicit grant flow available for [Webex Integrations](https://developer.webex.com/docs/integrations). Then, after authorizing the application, a meeting destination is entered and the Meeting Widget opens to that destination. Webex meeting destinations can be an email address, user ID, room ID, or SIP address.

You can view the source code of the starter application here: <https://github.com/WebexSamples/webex-meeting-widget-starter>.

#### Meetings Widget Vidcast

Checkout a quick Vidcast showing the Meeting Widget in action:


	<iframe src="https://app.vidcast.io/share/embed/29de8071-7f2d-4317-8ff1-169f8c22eb23" width="100%" height="100%" title="Webex Meetings Widget" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>


&nbsp;

### Your Feedback Matters

If you have feedback, suggestions, or you are encountering issues using the Meetings widget, please reach out to our support team <https://developer.webex.com/support>, and we will be very happy to help!


  [1]: https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta38920290ebf222c/61ddaa351757dc6aed2ae12a/main.png
