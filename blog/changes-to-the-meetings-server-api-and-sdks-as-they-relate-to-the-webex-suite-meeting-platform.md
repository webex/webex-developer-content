---
type: Article
title: Changes to the Meetings Server API and SDKs, as they relate to the Webex Suite Meeting Platform
canonical_url: https://developer.webex.com/blog/changes-to-the-meetings-server-api-and-sdks-as-they-relate-to-the-webex-suite-meeting-platform
content_type: blog
date: '2024-04-15'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/changes-to-the-meetings-server-api-and-sdks-as-they-relate-to-the-webex-suite-meeting-platform)

Hello Webex Developers! We're excited to announce significant updates to the Webex SDKs that streamline the process of starting and joining meetings in spaces. These changes are designed to improve your development experience and provide users with a more secure and integrated meeting experience.

As of the latest SDK release, we've streamlined the meeting functionalities within spaces, which means that starting and joining a space meeting is now more straightforward and consistent across the board. These changes affect our Webex [Browser/JS SDK](https://developer.webex.com/docs/sdks/browser), [iOS SDK](https://developer.webex.com/docs/sdks/ios), and [Android SDK](https://developer.webex.com/docs/sdks/android). To ensure a smooth transition, we've prepared comprehensive migration guides that walk you through the process step-by-step.

### What's New?

The recent updates introduce a unified method for handling space meetings, which simplifies the codebase and reduces complexity for developers. These changes are effective from the following versions of each SDK:

- Browser SDK **v2.60**
- Mobile SDKs **v3.11**

<br/>

### What to Expect

Here's a quick overview of what to expect for the migration:

- **Unified Meeting Objects:** We have unified the meeting objects for space meetings, which means that the steps taken in all the listed SDKs to work with meetings will be similar, regardless of whether you’ve working with space meetings or regular scheduled meetings.
- **Enhanced Security:** Meeting Password is now mandatory for non-invited guests.
- **Revised API Calls:** Starting and joining meetings now require the creation of meetings through the [/meetings](https://developer.webex.com/docs/api/v1/meetings) API, even for meetings in spaces. This is to align with how regular scheduled meetings are created.
- **Improved User Experience:** The updates offer a seamless user experience for participants joining meetings, whether they're using Webex on a browser, iOS, or Android device.

<br/>

### Migration Guides

To help you migrate to the new meeting in spaces experience, we have provided extensive migration documentation. Please refer to the following resources based on your development platform:

- Webex Browser/JS SDK Migration Guide: [https://github.com/webex/webex-js-sdk/wiki/Migration-to-improved-meetings-associated-with-a-space](https://github.com/webex/webex-js-sdk/wiki/Migration-to-improved-meetings-associated-with-a-space)
- Webex iOS SDK Migration Guide: [https://github.com/webex/webex-ios-sdk/wiki/Migration-to-improved-meetings-associated-with-a-space](https://github.com/webex/webex-ios-sdk/wiki/Migration-to-improved-meetings-associated-with-a-space)
- Webex Android SDK Migration Guide: [https://github.com/webex/webex-android-sdk/wiki/Migration-to-improved-meetings-associated-with-a-space](https://github.com/webex/webex-android-sdk/wiki/Migration-to-improved-meetings-associated-with-a-space)
- General Overview and Use Cases: [/docs/space-meetings-migration](https://developer.webex.com/docs/space-meetings-migration)

Each guide provides a detailed explanation of the changes, including code snippets and best practices to ensure that your migration is as smooth as possible. We’ll go into more detail on each one below.

### Get Started

Let’s get into it. We’ll highlight some of the main changes and how you can work through them. If you have any questions or are unsure about something, you can always reach out to the [Developer Support](https://developer.webex.com/support) team. For this blog’s purposes, we assume you’ve worked with our SDKs before and are comfortable with the technologies and terminology used. If you haven’t, check out our SDKs (and everything else we provide) on the [Developer Portal](https://developer.webex.com/docs).

We’ll start with the points that are common to all 3 SDKs, then move on to the specific cases and code snippets for each one individually.

### Create a Developer Sandbox

First, we recommend creating a developer sandbox to play around with and test this migration. The developer sandbox will come with all the usual features, but it will be created within the new Meeting Suite Platform, so that you can test these new features and see the changes compared to the old platform. Head over to the [space migration page](https://developer.webex.com/docs/space-meetings-migration) and create the sandbox request.

Once you request the sandbox, it will be set up in the background. This may take up to 24 hours.

### Test Out the APIs

Once you’ve created your sandbox, you should start by testing out the [Meetings REST APIs](https://developer.webex.com/docs/meetings) (herein referred to as *Meetings API*), to see what’s changed there. The changes are listed in the migration documents but let me give you the highlights below.me give you the highlights below.

#### Create a New Meeting

One of the main changes is that if you want to create a meeting from the context of a space through the API, you now will be creating the meeting within your own meeting site. In other words, the meeting creator’s licensing and site selection dictates where the meeting will be hosted. This is irrespective of whether you’re part of the space’s owning org or an external org.

Now, creating a meeting in a space through the API involves adding the `roomId` to the POST API request to [/meetings](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting) API. As mentioned, the licensing that the meeting creator has assigned determines the meetings site of the meeting, regardless of what org and site the space’s creator resides in.

Similarly, you’re also going to see that “Instant meetings” (created by adding the `roomId` and `adhoc=true` fields in the API) will be created in the API caller’s preferred meeting site and org, which again is not necessarily going to be the same meeting site as the space creator’s meeting site. These changes should be taken note of, to ensure smooth implementation. If you plan to get data on these meetings later (for example, reporting data), you will need to be part of the meeting site where said meeting was hosted.

The caveat to all this however, is if you’re using a [Service App](https://developer.webex.com/docs/service-apps) to create meetings. Service Apps work independently of any user, therefore when you create a meeting using a Service App token, you need to add the `hostEmail` parameter so that the backend logic can determine who the host user is and create the meeting on behalf of that user. That user’s licensing and site will then determine where the meeting is hosted and what capabilities it will have.



> **Info**
>
> The key change you’ll see is that you will not be able to use `roomId/spaceId` anymore within the SDKs to join meetings. You will need to use the `meetingId` or the SIP URI, both of which are found through the Meetings API.



#### Additional Points to Keep in Mind

One point to note is that in the scenario you have users within a space from multiple external organizations than your own (as the space creator), there may be a period where your org and site may be on the new Webex platform, but other attendees may not yet be on it. This can lead to slightly different experiences (both with the SDKs and native clients), but the overall usability shouldn’t be impacted. Of course, reach out to our [Developer Support](https://developer.webex.com/support) team in case of any queries or concerns.

### The Browser SDK

As mentioned above, the use of `roomId/spaceId` to join meetings has been removed. Instead, you’re asked to use the meeting’s *SIP URI* or `meetingId`, found with the Meetings API or by using [getAllMeetings()](https://webex.github.io/webex-js-sdk/api/#getallmeetings) directly in the SDK. You can check if a site is on the Webex Suite Meeting Platform from the SDK by querying the following key. The label “unified” is the shorter internal reference to WMSP meetings:

```javascript
webex.meetings.config.experimental.enableUnifiedMeetings
```

This is a boolean and tells you whether your SDK implementation is working on the new platform, by returning *true*. If you don’t get a value of *true*, you can set it to *true*. Of course, this is best taken care of after you init and then register.

Once you’ve confirmed that this toggle returns `true`, you can proceed to creating your meeting object as below:

```javascript
webex.meetings.create(“YOUR_DESTINATION”)
.then((meeting) => {
    console.log(meeting);
});
```

Pretty straightforward as you can see, the code is the same as before so no changes there. However, if you now enter your `roomId/spaceId` as the destination, you’re going to get an error message stating the following, “*Using the space ID as a destination is no longer supported. Please refer to the [verifyPassword() migration guide](https://github.com/webex/webex-js-sdk/wiki/Migration-to-Unified-Space-Meetings) to migrate to use the meeting ID or SIP address.

#### Verify the Meeting Password

As you probably know from the native client application functionality, if you are not part of a space, you generally won’t be able to join any meetings within it. However, there may be cases where you might like to have some users be part of a specific meeting within that space, without being a member of the space.

If that’s the case, then you usually need to safely share the meeting password with them. Then, when they authorize through the SDK, and the meeting object is created, they will be required to enter the meeting’s password. You can use the [verifyPassword()](https://webex.github.io/webex-js-sdk/api/#meetingverifypassword) function to subsequently verify the password entered by the user. Nothing new as it’s been around for a few releases already, but here is a quick code snippet showing how to use it.



> **Info**
>
> At this point the expectation is that the meeting object is already created, called `meeting` below.



```javascript
if (meeting && meeting.passwordStatus === 'REQUIRED'){
  meeting.verifyPassword('User_entered_PW')
  .then((res) => {
       if (res.isPasswordValid) {
         console.log('Password is verified');
       }
     })
    .catch((err) => {
       console.log('error', err);
   throw (err);
    });
}
```

It’s a simple code sample as you can see, but you can, of course, make it more robust by checking if a captcha is required for example, or any other combination of password and CAPTCHA. If you want to know more about this, you can check out [this wiki](https://github.com/webex/webex-js-sdk/wiki/Implementing-Password-and-Captcha-Verification-Flows) as it goes into more detail. Also, worth noting that if the user is not part of the space, they may still be put in the lobby until the host admits them. This may depend on the site’s security settings configured in Control Hub, see [here](https://help.webex.com/en-us/article/ov50hy/Webex-best-practices-for-secure-meetings:-Control-Hub) (search for “lobby”).



> **Info**
>
> Don’t forget that you can always invite participants to the meeting through the SDK, using the [invite](https://webex.github.io/webex-js-sdk/api/#meetinginvite) function within the meeting object.



#### Reclaim the Host

This is a newer feature within the SDK, that allows participants to reclaim the host role. The Migration Guide already does a good job of explaining how to use it, so I’ll just leave the link reference to it [here](https://github.com/webex/webex-js-sdk/wiki/Migration-to-improved-meetings-associated-with-a-space#reclaim-the-host-role).

Essentially, it’s using the [assignRole()](https://webex.github.io/webex-js-sdk/api/#membersassignroles) function and this allows you to set the role of the member/participant to “Moderator”, also passing the `hostKey` so that it can be validated.

At this point, once all the above is taken care of, you can consider your Browser SDK migration complete. As always, please ensure to test your company’s use cases (at least the most common ones) to confirm that all is working as expected. Testing is key to all we do as developers!

### The Mobile SDKs

This information applies to all our Mobile SDKs and therefore we’ll discuss them together.

The respective migration guides for each (here they are again for reference: [iOS SDK](https://github.com/webex/webex-ios-sdk/wiki/Migration-to-improved-meetings-associated-with-a-space) and [Android SDK](https://github.com/webex/webex-android-sdk/wiki/Migration-to-improved-meetings-associated-with-a-space) migrations) are detailed and provide some sweet code samples to help you get into it. We’ll highlight the key points for them, just to give you a point of reference.

#### Room/Space IDs are Gone Here Too

As with the Browser SDK, the main changes apply to how we’ve removed the ability to use `roomId/spaceId` to “dial” into a meeting. Now you must use either the meeting number, SIP URI, or meeting URL. As mentioned, the migration guides have detailed code samples for each OS.

Essentially, your `webex.phone.dial()` method should pass in one of the above as dial Inputs, along with the Media Options and `CompletionHandler`.

If you try passing a `roomId/spaceId,` you’re going to get a `CANNOT_START_INSTANT_MEETING`error. I’ve highlighted the same error below while debugging our [Android KitchenSink Sample App](https://github.com/webex/webex-android-sdk-example), to give you an idea. The [iOS KitchenSink App](https://github.com/webex/webex-ios-sdk-example) will also return the same error:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt75453313a0d014a8/space-meetings-migration-2.png)

And while on the KitchenSink app, it would be worth testing with that, if you’d like to check out these changes. It’s got all the bells and whistles of the SDK, including the new features we’re highlighting.

As an example, it also allows the user to manually choose which input to use to dial in, see screenshot below (again, on Android, but the iOS KitchenSink App has the same functionality). You can debug this in the app’s code and see what it actually does (exact code line for my breakpoint on the Android KitchenSink App is [here](https://github.com/webex/webex-android-sdk-example/blob/bd8568ce01829f71754102339f11533e15356f08/app/src/main/java/com/ciscowebex/androidsdk/kitchensink/WebexViewModel.kt#L388)). This serves as a convenient debugging tool, and you can use it to inspect the flows. Of course, in a production application this would be handled directly in the code logic without the need for manual processing, but you get the idea.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt406a231ad1ebd528/space-meetings-migration-3.png)

Moving on, the other significant changes are in how the meetings are created, and that’s by using the Meetings API, as explained earlier for the Browser SDK. So, we won’t repeat it here. Same goes for the user who creates the meeting, their licensing will dictate which meeting site the meeting will be hosted on.

### Other Features Worth Pointing Out

Here are some additional features available in the SDK:

- Password/CAPTCHA verification
- Join meeting as Host
- Reclaim Host Role
- Make another participant host
- Invite another participant

All those are detailed in the migration guides too, with clear code samples. And that’s the Mobile SDKs Migration!

### General Tips

Some tips that we’re sure you already know but are always worth being reminded of:

- **Review the Documentation:** Take time to carefully read through the migration guides to understand the changes and how they apply to your applications.
- **Test your Implementation:** Before rolling out changes to production, thoroughly test your updated code to ensure everything works as expected.
- **Stay informed:** Keep an eye on the [Webex Developer Blog](https://developer.webex.com/blog) and subscribe to our newsletter for the latest updates and best practices.

<br/>

### We're Here to Help!

We understand that migration to a new system can sometimes be challenging. Our team is dedicated to making this transition as smooth as possible. If you have any questions or need assistance, don't hesitate to reach out to us through the [Webex Developer Support channels](https://developer.webex.com/support).

Happy coding, and we look forward to seeing how you integrate these exciting new changes into your applications!

-- The Webex Developer Team
