---
type: Article
title: Getting Started with Guest-to-Guest Meetings - No Coding Required
canonical_url: https://developer.webex.com/blog/Getting-Started-with-Guest-to-Guest-Meetings
content_type: blog
date: '2024-09-30'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/Getting-Started-with-Guest-to-Guest-Meetings)

Are you intrigued by the brilliance of the Webex Suite? The legendary audio and video quality, the phenomenal virtual backgrounds that let you host meetings from the captain\'s chair of a SpaceX rocket, and the sleek, elegant experience of Cisco room devices! But then, you dive into the licensing details and find them a bit too rigid for your taste. You crave something more flexible, something that doesn\'t tie licenses to specific users. You\'re not looking for a minutes-based system either; predictability is key, and you don\'t want to wade through cumbersome monthly reports. Most of your users only occasionally need to conduct meetings, so what\'s the solution?

Enter guest-to-guest meetings!

Imagine full-featured Webex meetings between non-licensed users. No more binding licenses to individual names! The host is a Webex Service App orchestrating the meeting, giving you the flexibility you need. And the best part? There\'s a new guest-to-guest SKU, allowing you to pay only for the number of simultaneous sessions. With everything running through the central Service App, your code logic becomes simpler, making development and maintenance a breeze.

Intrigued? If your curiosity is piqued, read on for a quick walkthrough of this game-changing guest-to-guest functionality. We\'ll start from scratch and guide you through setting up a meeting between two guests in just a few simple steps.

A Quick Note on Hyperlinks

Most hyperlinks in this text are deep links. For instance, when I mention finding your guest site in Control Hub, I link directly to the page where the sites are listed. If deep linking isn\'t possible, I\'ll provide clear instructions on how to get there. In other words, make sure to take advantage of the many hyperlinks I\'ve included!

#### What you need

Before we dive into the magic of guest-to-guest meetings, here\'s what you\'ll need to get started:

1\. A Webex Account: You\'ll need an account to log in to the Developer Portal and request a [guest-to-guest (g2g) sandbox](https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide). Don\'t have an account? No worries! You can [sign up for a free](https://www.webex.com/) one in no time. ![Webex Signup Page](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9c0dffa00ff577ae/66ec850a164dbf42c75aff87/Picture1.png)

2\. The [Postman](https://www.postman.com/) API Tool: This handy tool will be your best friend for API calls. I\'ll be sharing a [Bruno](https://www.usebruno.com/) collection in my GitHub soon, so check back occasionally!

3\. GitHub Postman Repository: Make sure to access and download the WebexSamples GitHub [repository](https://github.com/WebexSamples/g2g-meeting-sample) specifically set up for g2g meetings.

4\. A Browser: Chrome, Safari, Firefox, Opera-take your pick! Personally, I like to keep things organized by using different browsers for my sandbox *developer* and sandbox *admin* roles (Safari and Firefox), but feel free to follow your own style. Wondering where the admin fits in? Hold tight; the wonders of our sandbox and Service Apps are about to unfold!

5\. Node.js: If you\'d like to use a simple script I created to launch Chrome tabs from Postman, you\'ll need [Node.js](https://nodejs.org/en/download/package-manager). This script makes it a breeze for guests to join the meeting via the Webex web interface-one tab per guest.

Here is what we are working towards. This is a meeting between a Dr. and a patient in Webex (both me from the same camera feed) -- neither is licensed for meetings. This happens in a browser for simplicity, but it translates to the SDKs and Widgets, which we will show you later.

![Dr. and Patient meet - neither is licensed for Webex -- The Small insert is The Self View](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt17f32be910184fef/66ec850aff82bd7f682d18ad/Picture2.png)

If you\'re thinking, \"I\'ve seen this experience a million times,\" you\'re absolutely right-and that\'s the beauty of it! We\'re not here to reinvent the meeting experience itself. Instead, we\'re transforming the way you get there. With minimal coding required, we\'re offering a scalable solution that\'s fully compliant with the Webex Suite Meetings Platform. It\'s all about making your life easier while delivering the seamless, high-quality Webex experience you know and love.

#### Request A Sandbox

Ready? Let's go. We'll start working with our sandbox. After you requested your sandbox, you should have received a welcome email with instructions on how to access it. The sender is <cortex@wbx.ninja> if you want to check your spam folder. Use your admin credentials to log in to [Control Hub](https://admin.webex.com/).

![Sample welcome email for your new sandbox](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2b86fa9796cd7849/66ec850a3429370b67a17495/Picture3.png)

Let\'s dive in and check out your sandbox to see that a g2g site is all setup and ready for us to use. You can check this in [the site list](https://admin.webex.com/meetings/site-list). Here is how mine looks like. Notice the *Guest-to-Guest site* label under Additional Information? That's just what we expect. If you don't see it you may have requested a regular sandbox, right now g2g sandboxes are different from suite sandboxes, but we'll merge them soon.

![Guest to Guest site Preconfigured in the Sandbox](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc1686bdfd78c4f0e/66ec850ae6c606242fa802db/Picture4.png) 

#### Create a Developer User

Next, we\'ll [create a developer user](https://admin.webex.com/manage-users/users). The developer will then craft the [guest-to-guest Service App](https://developer.webex.com/my-apps) in the [Developer Portal](https://developer.webex.com/), and the admin will give it the green light using the [Control Hub GUI](https://admin.webex.com/apps/service-apps). The best part? In your sandbox, you get to play both roles!\
\
I\'ve deep linked all the relevant sections above, making the process self-evident with our intuitive Control Hub GUI. Once you\'ve created the developer user, they\'ll receive a welcome email with instructions to activate their account-essentially, just log in and set a password.

####  Create the Guest-to-Guest Service App

Now we\'re getting to the exciting parts! In the Developer Portal, [create a new app of type \"Service App.\"](https://developer.webex.com/my-apps/new/service-app) Fill in the fields and select one of the default app logos. The name of the Service App may show in the meeting roster of some of the clients. Use a name you don't feel embarrassed about later. More importantly, let\'s focus on the scope list. At a minimum, I recommend including the following scopes:

• *meeting:schedules_read*

• *meeting:schedules_write*

• *meeting:preferences_read*

• *meeting:preferences_write*

• And the most crucial one: *guest-meeting:rw*

The *guest-meeting:rw* scope identifies this Service App as a guest-to-guest Service App, granting it special privileges and a tailored flow in the Control Hub approval process, where a guest-to-guest site must be selected.

If you want to use the SDK demo, you need to ensure the Service App can create guests. You can do this by selecting these additional scopes:

• *guest-issuer:read*

• *guest-issuer:write*

After creating your Service App, you\'ll be presented with the *clientId* and *clientSecret*. You can store the secret now or recreate it later-either way works. However, you must submit your new Service App for admin approval. Simply click the \"Request Admin Authorization\" button to do this.

![Request admin authorization makes the service app visible to the admin in Control Hub](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd0de38fb4e615ce6/66ec850a164dbfccaf5aff83/Picture5.png)

#### Authorize the Service App

Now it\'s time to use your sandbox admin account to approve the g2g Service App. Log in to the [Service Apps approval site](https://admin.webex.com/apps/service-apps), select the newly created Service App, and authorize it. During the authorization process, it will automatically select the guest-to-guest site for you. There\'s a one-to-one mapping between a g2g Service App and a guest site.

![Authorize guest-to-Guest Service App](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf02af2607f84f747/66ec850afa6ba410ae0c9c6b/Picture6.png)

If you later create another Service App with the guest-meeting:rw scope and want to authorize it, you\'ll first need to release the current guest-to-guest site. If you want several guest-to-guest sites for your customers in one org, you can purchase multiple subscriptions and run them in parallel, each with their own assigned Service App.

#### Retrieving the Token

Okay, we\'re almost there-just one last step before the real fun begins! The developer needs to retrieve the token for the Service App, which will be used to orchestrate and manage the g2g meetings. Head over to the Developer Portal and navigate to your Service App page. Look for the \"Org Authorizations\" segment. If you don\'t see it, simply refresh the page.

![Retrieve Access Token for g2g Service App](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1073fc03aac599d5/66ec850ade00f91bf50e3dcc/Picture7.png)

Select your sandbox organization from the dropdown list (there should be only one), and then copy the *clientSecret* into the field to generate the *access* and *refresh tokens*. Finally, copy the access token for use in your Postman collection.

#### Wrapping Up the Prep Work

There is one more thing we want to do. We want to enable meetings between only guests. This is so no one has explicit host control over the meeting. If you want a guest to be the host, you can use the *startLink* instead of the *joinLink* later in the Postman flow.\
\
To allow meetings between only attendees select your [guest site in Control Hub](https://admin.webex.com/meetings/site-list). Click it. Select "All" and "Security".

![Site Configuration in Control Hub. Sites -- All - Select Security.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt35b7eaa2efa81fde/66ec850a9ae20520b96859b4/Picture8.png)

Make sure you select the "They can join the meeting" under the Webex Meeting Security Section.

![Allow guests to join](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt268c071838242693/66ec850a88368053ddc3d30b/Picture9.png)

Select the right settings for "Join before host."

![Allow Guests to join without the Host](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltfddb91f510cd0221/66ec850a8d84784a08304c56/Picture10.png)

So far, everything we\'ve done is just the prep work. If you\'ve used Service Apps before, this process is probably second nature to you, and you\'ve likely gone through it many times. That\'s another advantage of our g2g offering-it builds solidly on top of existing concepts and frameworks. There\'s very little that\'s new here, yet we\'re able to create a powerful, new and innovative solution.

### Use the SA Token to orchestrate g2g meetings


#### Start the helper script

Now, let\'s move on to the exciting part! With our Service App token in hand, we\'ll quickly schedule a meeting. We\'ll create a join link for each guest, allowing them to join the meeting with a simple click through their browser.\

If you want to make use of the script, I wrote that opens the browser tab with the *joinLink* you need to start it with\
\
node runChromeTab.js\
\
The script, like the Postman collection, is part of the [repository](https://github.com/WebexSamples/g2g-meeting-sample) I linked to earlier.

#### Import Postman Collection and configure Access Token

First, let's set a new and empty environment for the Postman collection. Go to the "Environment Quick Look" icon on the right side and add a new one.

![Postman environment Variables Quick look](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb76f10699c9c02c7/66ec8834f4d6ab471b6d379a/Picture11.png)


![Postman create a new environment for Advanced functions in the collection](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt363ede9ec087c61c/66ec8835a924ba67e7df57d5/Picture12.png)

Next import the g2g Collection into Postman

![Import the g2g collection into Postman](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4e9f211e36730cde/66ec8835c8a41630aba9893f/Picture13.png)

When the Collection is loaded copy your access token into the Collection's authorization. Ensure Auth Type: Bearer Token is selected. All API requests will be done with this g2g Service App token. Press Save for Postman to use this token.\
\
![Set the Service App Access Token for the Collection](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8ddd082dbfb925c0/66ec8835790a3d125cdd78e1/Picture14.png)
\
Verify that your token is configured correctly by executing the **GET Service App meeting preferences API call** -- You should see a response similar to the following.\
![Assert Validity of access token by calling meeting preferences on the Service App](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt34acb4ceeccc2e49/66ec8835fa6ba401b90c9c7f/Picture15.png)

### Schedule Guest to Guest Meeting and join Guests

If this worked, you are almost there. We only need to do two more things

-   Have the Service App schedule a meeting via the meetings REST API

-   Join guests to the meeting with the meeting joinLinks

Scheduling the meeting is done via the Postman **POST Service App creates guest-to-guest meeting .**

![The Service App Schedules the meeting](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt225a6816e11338b2/66ec883436f3bd00e4407885/Picture16.png)

Just send the request via Postman. There is some Javascript magic going on. Meetings are always scheduled in 15min intervals past the hour (xx:00,xx:15,xx:30,xx:45) and run for half an hour. Scheduling them so close to the current wall time means we can join them right away.

Use the Service App to create the *joinLink* by executing the

**create guest 1 join link and join as attendee** in Postman.

If you have the JS script running it will create a *joinLink* pass it to the script and the script launches a Chrome tab with the link. If you get an error you may not run the JS script I mentioned, and you need to copy the *joinLink* manually from the Postman response and copy it into a browser tab.\
\
When you see this dialog press "Cancel" and then "Continue in this Browser".![Click Cancel - We will meet in a browser tab](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt766d41e92ffc7d38/66ec88342c6c3cf42671e784/Picture17.png)

![Continue in this browser will open a Tab with the meeting experience](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt207ca2c6f298a2c1/66ec8834acf78ecf04c0e7ba/Picture18.png)

You may need to approve microphone and camera access. Then you should be in the meeting.\
Here is how it looks after the first guest joins and with video turned off so you can see the guests name.

![First guest joined - you need to approve audio and video access in the browser when prompted](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4311c31b0c885bdb/66ec88341d1e95fe6b22901d/Picture19.png)

Call the Postman API **create guest 2 join link and join as attendee** to join the other guest ( here the Dr. ) in the same way.

Huzzah! You have your first g2g meeting running live. None of the participants are licensed. In fact, you can schedule and start as many meetings as your Service App is licensed for, each with two or more guests.

### Wrapping up and Trying out the SDK

We\'re essentially done, but I promised one more thing if you want to try out the SDK. We\'ll use the [KitchenSink JS App](https://webex.github.io/webex-js-sdk/samples/browser-plugin-meetings/), a modular frontend to the JS SDK. To launch the SDK, you\'ll need an identity (a person ID), which we don\'t have yet. If you selected the *guest-issuer:read/write* scope earlier for your Service App, you can proceed right here. If not, you\'ll need to update the scope list, add the necessary scopes, then deauthorize/authorize and retrieve a new access token to use in the Postman collection.

Once you are ready call this API in Postman

**Service App creates guest 1**.

You will see an output like this\
![Create a guest identity to launch the SDK](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4daca2e19b170a77/66ec88348d84787a17304c8e/Picture20.png)

Copy the guest *accessToken*, then head over to the Kitchen Sink App and insert it before calling Webex.init()

![The guest Access Token is used to init the SDK](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc74f6405a1cad291/66ec884b0ebcddaf68f09a0b/Picture21.png)

A button will turn green to allow you to register your SDK/device to the Webex cloud. Do it.

![The SDK registers liker a device](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf38700cee4cff585/66ec884b76bb2e7dba9c8fbe/Picture22.png)

We are now registered as the guest with Webex. All we need to do is find and join our meeting. There\'s a section called \"Manage Meeting\" in the Kitchen Sink App. I found it easiest to use the meeting\'s *sipAddress*. In your Postman collection, locate the API response body where you scheduled the meeting, copy the *sipAddress*, and insert it into the Kitchen Sink app.\
\
![Retrieve the meeting\'s SIP address](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt46e07acd0b734bbf/66ec884bc8a416109ba98943/Picture23.png)

Press Create Meeting and then radio-button-select it.

![Find the meeting. Create Meeting will find it. Then select the radio button](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt64fe8fea836a5677/66ec884be2f8762c22404261/Picture24.png)

In the \"Join Meeting\" section, copy your password from the Postman response and verify it. Once that\'s done, you can join the meeting from the SDK as a guest by clicking \"Join With Media.\"

That\'s it-you should now have three guests in the same meeting!!![Join the meeting with Media](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8e726b425ae0fb69/66ec884b8d84780355304c93/Picture25.png)

![SDK Kitchen sink is connected to the meeting](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5e30de85c4a96af1/66ec884b1ad0c133ac4b25cb/Picture26.png)


![3 guests in the meeting](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt40a492d3b9ae0dfc/66ec884b497b074b429fce53/Picture27.png)

The only thing that has changed here is how we join the meeting. The guest-to-guest Service App is still the orchestrator and license sponsor.

### Conclusion

Thanks for sticking around until now. As promised, we started with nothing and ended with guest-to-guest meetings where non-licensed temporary users can freely meet. We spent most of our time on setup, but to get a g2g meeting running, we used only one API call for the Service App to schedule a meeting. You can repeat this for as many meetings as you like. Meetings in progress are counted against the Service App\'s maximum limit.

We believe this new offer and new ordering SKU will unlock new use cases and enable customers who previously relied on space-backed meetings to easily port their applications.

If you have any questions, feel free to reach out to support at devsupport@webex.com or to me via Webex-devex@cisco.com.
