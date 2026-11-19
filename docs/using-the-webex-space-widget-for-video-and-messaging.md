---
type: Guide
title: Using the Webex Space Widget for Video and Messaging
display_title: Using the Webex Space Widget
canonical_url: https://developer.webex.com/docs/using-the-webex-space-widget-for-video-and-messaging
content_type: documentation
product_group:
- webex-suite
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/using-the-webex-space-widget-for-video-and-messaging)

## Objectives

In this demonstration, you’ll learn more about the Webex SDKs and Widgets capabilities, and experience these through live demos of the [Space Widget](https://developer.webex.com/docs/widgets#space-widget).

## Pre-requisites

To complete this tutorial you will need a Webex user account. You can [create](https://www.webex.com) now if you don't have one. As this tutorial demonstrates using the Spaces Widget to quickly create a collaboration session with other users, ideally you will have another Webex account (a friend or colleague, for example) to invite. Or you can create a second create a second Webex account with a secondary email address.

## About the Webex SDK and Widgets

Webex brings people together to collaborate, discuss, and make decisions in instant and scheduled meetings. In-app, high-quality audio/video calling pulls the people in Spaces together with one tap from the desktop and mobile Webex clients.

![Video participant](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt73867c74422a18ed/61e8807ec5ff2e754efb0e8f/awesome-video.png)

Whether in field service, remote healthcare, distance learning, financial services, retail or enterprise collaboration, there are many situations where you may want to embed Webex messaging, meeting and audio/video calling capabilities into existing applications - without the requirement to install a separate Webex client.

This is where the Webex SDKs and Widgets come into play: leveraging standard codecs and protocols like H.264, WebRTC and SIP, developers can easily and securely render video calls and messaging in Web and Mobile applications.

![Embedded video running in web and mobile apps](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt0e74b4995a6e45d2/61e8807e67d4b03377be4300/embedded-video.png)

## Webex SDKs

The Webex SDKs let mobile and web developers leverage the Webex user experience and customize it to their needs.

With the SDKs, you get fine-grain control of the user experience and how the video/messaging/meeting capabilities are presented. The Webex SDKs let you initiate calls (to other Webex clients, phones and rooms, PSTN numbers or SIP URIs) and receive/answer incoming calls, perform 1:1 and group persistent chat, and join Webex meetings.

The [Webex SDKs for iOS](https://developer.webex.com/docs/sdks/ios), [Android](https://developer.webex.com/docs/sdks/android) and [Browser](https://developer.webex.com/docs/sdks/browser) are accessible from the [Webex for Developers](https://developer.webex.com/) portal: they comprise API references, quick-start guides and a sample applications.



> **Info**
>
> Full source code for Webex SDKs is available on [GitHub](https://github.com/webex/react-widgets).



### Widgets for web applications

The Webex Widgets are the quickest way to integrate the Webex user experience: by pasting a few lines of HTML and Javascript code, you will be able to bring calling, messaging and meeting features to existing Web applications. The widget provides a full Webex UI experience within its container (as defined by the web page author).

The [Webex Widgets](https://developer.webex.com/docs/widgets) are responsive [React](https://reactjs.org/) based components that embed audio/video calling (dialing by email, SIP URI or DTMF), and provide optional JavaScript events providing integration opportunities with the rest of the page UI.  They offer a full persistent messaging experience (with markdown, message-flagging, file-sharing, etc.) as well as the ability to participate in Webex cloud meetings.



> **Info**
>
> Full source code for Webex Widgets is available on [GitHub](https://github.com/webex/react-widgets).



The Webex Widgets come in two flavors: the [Space](https://github.com/webex/react-widgets/blob/master/packages/node_modules/@webex/widget-space) Widget and the [Recents Widget](https://github.com/webex/react-widgets/blob/master/packages/node_modules/@webex/widget-recents).

Next, you’ll experience using the Space Widget.
## Experience the Space Widget

The Space widget handles coordination between your application and the Webex APIs: it provides fully functional, ready-to-use components of the Webex meeting user interface ready to drop into you existing web page.

The Space widget (as of this writing) supports the following features:

* 1-on-1 and group space messaging
* 1-on-1 and group space video calling
* Space roster list and @mentions
* Dialing by email address or SIP address
* Inline Markdown formatting
* Sharing of files and documents
* Previewing and downloading of files and documents
* Flagging messages for follow-up



> **Info**
>
> Whiteboard features are not supported by the current version of the Widget.  See the [Widget GitHub repo](https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-space) for the latest details on feature/browser support.



The demo requires two inputs:

* A Webex API access token.
* The ID of a Webex meeting, or the email address of a Webex user, with whom to start a collaboration session

**To experience the Space widget:**

1. Sign in to the [Developer portal](https://developer.webex.com).
1. Go to the [Accounts and Authorization](https://developer.webex.com/docs/getting-started#accounts-and-authentication) section of the [Getting Started](https://developer.webex.com/docs/api/getting-started) page. 

1. Click the copy icon at the right of the "Bearer ****" text field to copy your personal access token to your clipboard.

    ![Personal access token](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2b104c66a752a7dc/61e8807eb7138d58986f5636/webex4devs-access-token.png)

1. Using Firefox, Google Chrome or Safari, navigate to the [Space widget demo page](https://code.s4d.io/widget-demo/production/index.html).

1. In **Webex Access Token** panel, select **Access Token**, and paste your access token into the **Token** field:

    ![Pasting access token](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb134c10538a4c6f6/demo-form-token.png)

1. Click **Save Token**.

1. In the **Space Widget** panel, make the following selections:

    * Set **Widget Destination Type** to **To Person**.
    * Set **Widget Initial Activity** to either **Message** or **Meet**.
    * Under **Widget Activities** select all activities.
    * Under **Widget Composer Actions** select **Attach Files**.

    ![Selecting widget options](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte23805f2c20a157e/demo-form-select-options.png)

1. In the **Widget Destination** field, enter in the email address of the Webex user you wish to start the collaboration session with.  

    ![Email of user with whom to collaborate](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltddc7522e14c1ce87/61e8807ea1a3da10d297ccc9/demo-form-choose-id.png)
    
    Notes:
    * If you don't have another Webex user to call, you can enter `loopback@rtp.ciscotac.net`, or create a second Webex account using an alternate email address. This will let you send messages to the loopback user, but you won't be able to make a video call, for which you need to specify a real Webex user.
    * Don't use the same Webex account to both obtain the access token and use as the Widget destination as you can't call yourself!

    Now you’re ready to test!

1. Click **Open Space Widget** to experience the Space widget live in 1-on-1 mode. 

    

> **Info**
>
> If you don't see the widget, scroll down on the page. Click "Stick Widgets" to have the widget appear at the top of the page.



1. Post a few messages, drag-and-drop a file into the Space, and confirm that these activities are reflected in the destination user's Webex client.

1. Click the green call button in the upper-right corner initiate an video call.

    You’ll be asked for the authorization to access your camera and microphone.

    

> **Info**
>
> Note that you did not need to install any additional software to have the video call, as the Space widget takes advantage of standards-based [HTML5 WebRTC](https://webrtc.org/) functionality built into the browser to handle all audio/video functions.


## Add the Widget to an HTML page

In the previous steps, you experienced the messaging and video capabilities of the Space widget in a 1-on-1 Space.  We'll now show you how developers can add the Widgets into existing web sites and applications.

The Space Widget Demo page you just used to test your Widget also displays a sample code snippet pre-populated with your configured options, ready to copy-and-paste into a web page.  

Let's give it a try:

1. On the Widget demo page, scroll down to the **Space Widget Example Code** section.

1. Examine the sample snippet, which includes an HTML `<div>` element that will act as the Widget container, along with some JavaScript code that instantiates the widget on page load:

    ![Example generated code snippet](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9d19e986ef7d8496/61e8807e78c11410d82de322/code-snippets.png)

1. Using your favorite text editor create a new file named `widget.html`, and copy/paste in the example code into the page body.

1. Replace the `'XXXXXXXXXXXXXXXX'` place holder with your personal access token retrieved previously, and save your changes.

1. Open the `widget.html` file in a Web browser, and start collaborating!



> **Warning**
>
> Note that in a real-world applications you should **not** hard-code access tokens into your web application in this way. For production apps, [Webex Integrations](https://developer.webex.com/docs/integrations) provides the mechanism to securely authenticate users and obtain access tokens dynamically and safely.



## Going further

In this demonstration we’ve just scratched the surface of the experience the Space Widget can deliver. For example, the Space Widget can enable your web app to respond dynamically to [Widget events](https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-space#events) (e.g. answer an incoming call),
[control the Webex features](https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-space#configuration) that are offered in the UI, specify whether to start in messaging mode or jump directly into a video session, and more. Check out the [Widget README](https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-space#incoming) for all details.

In addition to basic 1-on-1 calling demonstrated in this tutorial, the Space Widget can fully participate in group/multi-user Webex meeting meetings and standard Webex meeting events, right from within your web application page.

To try this out, simply set the **Widget Destination Type** to **To Space** in the Space Widget demo app, and paste in the unique roomId of an existing Webex space.



> **Info**
>
> If you add **roomid@webex.bot** to a Space and it will automatically look-up the Space's `roomId` and send it to you in a 1-on-1 message.



![RoomId bot in action](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt76657f6c544a84ae/61e8807ed4cd11754d7c2de3/roomid_bot.png)

Finally, note there is another helpful Widget we haven't even touched on yet!  Discover the [Recents Widget](https://github.com/webex/react-widgets/blob/master/packages/node_modules/@webex/widget-recents).
