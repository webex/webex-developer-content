---
type: Article
title: Developer Sandbox Now Available
canonical_url: https://developer.webex.com/blog/developer-sandbox-now-available
content_type: blog
date: '2022-05-18'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/developer-sandbox-now-available)

A Webex Developer Sandbox unlocks the ability to make Webex API calls that require [Admin](https://developer.webex.com/docs/admin) user permissions, or to manage a licensed Webex organization using Webex Control Hub. Once access to a licensed org is granted, you can create and test [Webex Embedded Apps](https://developer.webex.com/docs/embedded-apps). What are the necessary steps to request access to a developer sandbox? Below we will go over the process for obtaining a Webex Developer Sandbox and its implementation.

### Requesting a Developer Sandbox

Once logged into the [Webex Developer Portal](https://developer.webex.com/) you can navigate to the [Developer Sandbox](https://developer.webex.com/docs/developer-sandbox-guide) documentation and click the **Request a Sandbox** button. You will be prompted to accept the Terms and Conditions prior to submitting the request. After a few minutes you will receive an email with the credentials needed to log into Control Hub for your new test organization.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt611494d10c3e7d09/6284184de2c49854288809dc/developer-sandbox-blog-1.png)

### Signing in to Control Hub

It is recommended that when accessing [Control Hub](https://admin.webex.com/login) that you use a private or incognito browser window to perform the sign in to avoid any potential conflicts with your primary Webex account. Simply enter the credentials that were provided in the email that was sent when the request for a Developer Sandbox has been approved. Once successfully logged in to Control Hub, if you want to make calls against the Webex [Admin APIs](https://developer.webex.com/docs/admin), you can open another tab within the private incognito browser session that you used to login to Control Hub, go to the Webex Developer Portal and select the login button and provide the provided credentials to sign in as the Admin user of the new test Webex organization. This will allow you to access a bearer token with permissions to make calls against the Webex Admin APIs or register an Embedded App for testing in the test organization account and submission to [App Hub](https://apphub.webex.com/).

### Creating a New Webex Embedded App

While logged into the Webex Developer Portal, you can click on the **A** icon in the top right corner of the screen. Then select the **My Webex Apps** option.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb389dd6c974401b5/6284184dfa2a685899864643/developer-sandbox-blog-2.png)

Next, click the **Create new App** button and select the **Create Embedded App**&#xa0;button from the app type options.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1a4a44f5c7a15e51/6284184d466b1b559357c07e/developer-sandbox-blog-3.png)

Here you will be required to provide the following information about the potential Embedded App:

- Identify if the Embedded App is intended to work in Meeting, Spaces, or both
- A name for the Embedded App
- A description of the Embedded App
- Upload or select an icon
- Include valid domains to be included as links in your Embedded App
- A start page URL that the initiator will load in the client before sharing the app
- Both in meeting start page URL and/or a messaging start page URL
- Select a layout preference for user experience

Once you have successfully provided all the required data, you can click the blue **Add Embedded App** button to finalize registering the embedded app and be prompted with a congratulatory message.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt0ca49a3ec450a466/6284184dd5f9386926e63a3a/developer-sandbox-blog-4.png)

### Enabling Your Embedded App for Testing

In Control Hub, on the left side of the screen in the Management section select the [Apps](https://admin.webex.com/apps/general) option.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltec932edd57a8de99/6284184dbdec0b542e4ef89c/developer-sandbox-blog-5.png)

Then select Embedded Apps and go to the Private Section of listed Embedded Apps and enable the **Show In-development apps** option.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt63cb820d5608b19e/6284184daf7b396927edc365/developer-sandbox-blog-6.png)

Finally, log into the Webex client using the administrator credentials. If you have selected the options for an in-Space Embedded App, you will be able to see the app listed as an option for use by the test org’s administrator by selecting the apps option from a Space in the Webex client.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbe2a1c8ccab925c1/6284184de2af4f67e9980e63/developer-sandbox-blog-7.png)

### Engage With Us

The [Webex Developer Community](https://community.cisco.com/t5/webex-for-developers/welcome-to-the-webex-for-developers-forum/m-p/4558386#M321) has dedicated topics, discussion groups, and announcements. We encourage you to tell us about your experience setting up a Webex Developer Sandbox.
