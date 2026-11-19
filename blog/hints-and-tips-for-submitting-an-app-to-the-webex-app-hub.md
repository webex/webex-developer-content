---
type: Article
title: Hints and Tips for Submitting an App to the Webex App Hub
canonical_url: https://developer.webex.com/blog/hints-and-tips-for-submitting-an-app-to-the-webex-app-hub
content_type: blog
date: '2023-03-22'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/hints-and-tips-for-submitting-an-app-to-the-webex-app-hub)

Many developers have worked on building a Webex [Integration](https://developer.webex.com/docs/integrations), [Embedded App](https://developer.webex.com/docs/embedded-apps), or [Bot](https://developer.webex.com/docs/bots) leveraging the various SDKs, APIs, and frameworks available on the Webex Developer Portal. Teams have spent time reading step-by-step [tutorials](https://developer.webex.com/docs/tutorials), watching [Vidcast](https://app.vidcast.io/collections/share/97163a12-e567-413c-9eb6-bdcad681d4c3) recordings around all the developer solutions available within the Webex Developer Platform and testing out apps. We appreciate the time and effort spent on creating something that adds value to the Webex end-user experience.

### The Webex App Hub

The Webex App Hub enables developers to share their Bots, Integrations, and Embedded Apps with the rest of the Webex Community. The App Hub is a marketplace, where Webex users and Admins can shop for potential value adds to the Webex experience.

The Developer Portal is stocked with guidance in the documentation around [submitting an application](https://developer.webex.com/docs/app-hub-submission-process) for listing in the Webex App Hub. Even though these processes are well documented, there are still nuances that are difficult to capture on paper. Below is an attempt to outline some of the common mistakes seen in App Hub Submissions and how to avoid them for a smooth and easy App Hub Review experience.

### The Submission and Review Process

Once a developer decides their application is ready for public consumption, and they want to list their app on the Webex App Hub, they would click the button labeled “Submit to Webex App Hub” on the application’s registration form.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6a8196742d44f47d/641b47b88fb92c3c39ea94ef/hints-and-tips-for-submitting-to-app-hub-1.png)

This would subsequently open a ticket that would prompt a response from the [Webex Developer Support Team](https://developer.webex.com/support) letting the submitter know that we will begin the review process. Then, a member of the App Hub Review Team will tell the submitter they are starting the submission review process.

The first step in the process is the Business Review. During this review, the App Hub team validates... When the Business Reviewer needs changes to be made, the submitter will get an email with the request. The review process is transparent and quick depending on how often the submitter checks and responds to the email thread. When the Business Reviewer is satisfied with the items on the registration form required for the App Hub listing, the Technical Review will begin.

The Technical Review stage is where the App Hub team tries the app using demo Webex accounts. We will add the bot to a space, spin up a Webex Meeting or Space to try out an Embedded App, or kick off the OAuth 2.0 grant-flow for an Integration. We will test its functionality thoroughly. There will be a subsequent email exchange with requests for required changes to be addressed by the submitter prior to being listed on the Webex App Hub. 

Below is a list of items that cause the most noise in this process.

#### Embedded App, Bot, or Integration Name

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3d24593e886c1828/641b47b840327e23a30cd689/hints-and-tips-for-submitting-to-app-hub-2.png)

Do not include the words “Cisco” or “Webex” in the submitted app’s name. If you must use these words in the title, please use them at the end. For example, “My App for Webex”. But, to ensure a smooth review experience, just leave the words “Cisco” and “Webex” out of the name.

#### Logo

This will be displayed on the App Hub in reference to the submitted app. Make sure it is a custom logo with no Webex or Cisco branding included. And your logo dismenions must be 512x512, if they aren't. The upload will fail. 

#### App Hub Description

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6ec4b27b55053807/641b47b849e8cc4fc47ba180/hints-and-tips-for-submitting-to-app-hub-3.png)

This is the part of the submission that is the noisiest in the review process. Below is a cheat sheet on the 5 main things we are looking for in this section.

1. A short sentence about your organization. For example, “My Org specializes in productivity and collaboration services that helps the world be more effective.”
2. A short sentence describing the Integration/Embedded App/Bot. For example, “My App is a Webex integration that enables sales teams to sell more in Webex Meetings.”
3. A list of benefits Webex users will experience by using the Integration/Embedded App/Bot.
4. A sentence that starts with “To use My App, …” followed by a set of pre-requisites a Webex user will need to get started with using the Integration/Embedded App/or Bot. Do users need to have an account with your organization? Do users need to have a paid or free Webex Account?
5. If the app is not an entirely a free service, we always ask to add an additional sentence that includes where to find more information on pricing. If you do not want to release this information publicly, then you can say something like “please contact our sales team at example.com for questions on pricing.” If the app is a free service, then say that explicitly here.

One other thing to note is that this section uses Markdown. If the “M” markdown bot is blue, editing is not allowed as this means the description is in preview mode. Click the blue box to take it out of preview mode and unlock the ability to edit the text.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8942ed6cb1fcfa81/641b47b88fb6853b8741bf4b/hints-and-tips-for-submitting-to-app-hub-4.png)

&nbsp;

#### Integration Scopes

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2e6f46fe7f52753a/641b47b80dc0a6102c4326ec/hints-and-tips-for-submitting-to-app-hub-5.png)

We ask that when selecting scopes for an Integration type submission that you select **Minimum necessary scopes**. But one thing that happens often here is that developers select `spark:all` when initially setting up the integration and forget to deselect this scope when submitting. Then, in the review process we ask for this item to be changed and the integration breaks because underlying API calls were dependent on this scope. We cannot approve an app that has the `spark:all` scope selected. Once scopes are selected, the submitter can scroll up the registration screen and click the “Submit to Webex App Hub” button.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt63080137ca521354/641b47b8f2a10e3b5426c616/hints-and-tips-for-submitting-to-app-hub-6.png)

&nbsp;

#### Summary

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd36d7db03d3eed12/641b47b8d9f2671f0a4c0d18/hints-and-tips-for-submitting-to-app-hub-7.png)

The Summary is the set of text that will appear below the app name on the App Hub. This needs to be a unique string of text. Often what happens is the submitter will copy the first line of the App Description (see above) and paste it into this field. Please make sure that this is a separate and unique string of text than any of the text that was placed in the App Description.

#### Categories

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf09c5cbc7d318fdb/641b47b80c2596708b32e803/hints-and-tips-for-submitting-to-app-hub-8.png)

You can select up to three categories for the app to be listed in the App Hub. Users will filter through apps on the App Hub by selecting these categories. If the organization you represent is not a member of the [Cisco Solutions Plus](https://developer.cisco.com/ecosystem/dnsp/) program, please do not select the “Partner Solutions” category. When a submitter selects this option, the review team does a check to confirm membership into the program. The check can take some time. Then, if the Review Team determines that a submitting organization is not in the program, they will have to ask that they remove the selection.

#### Landing Page

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt37245024836d3e0c/641b47b8361c5a5827e85d0d/hints-and-tips-for-submitting-to-app-hub-9.png)

The landing page needs to be publicly accessible and not behind any authentication path. It also needs to be a page on the submitting organization's website that is dedicated to the integration/Embedded App/Bot. The home page of your organization's main app will not satisfy this requirement. There are also some branding guidelines to adhere to on this page. If Webex or Cisco logos are used, they need to be the most up to date versions of the logos. When spelling Webex, make sure it is “Webex” and not “WebEx”. All branding guidelines for the landing page can be found [here](https://resources.webex.com/webex/integration-partners?guest_pw=ee9ec6b533f59d511dbf94f7599c8c043294ae11111c71c5e3945aec2032c43b).

#### Contact

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt64719a9e8f3137b6/641b47c27b579c3cb6681b15/hints-and-tips-for-submitting-to-app-hub-10.png)

The contact information on the submission form will never be publicly listed. This is the name and email of the person responding to requests from the Webex App Hub Review team when asking for changes to the submission. Please make sure that the contact listed here has access to the account that is logging into the Webex developer portal and the submission itself. Often what happens is there is a generic email placed here like support@example.com or engineering@example.com. When this happens, the App Hub Review team reaches out for changes to be made on the submission and the emails are ignored or not forwarded to the proper team for making changes. This can cause a Bottleneck in the review process.

### Need Some Help? We Got You Covered!

We are excited to provide you with support for your App Hub submission. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to point you in the right direction. You can also start or join a conversation on Webex for [Developers Community Forum](https://community.cisco.com/t5/webex-for-developers/bd-p/disc-webex-developers).
