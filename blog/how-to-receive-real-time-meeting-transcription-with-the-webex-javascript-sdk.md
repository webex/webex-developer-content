---
type: Article
title: How to Receive Real-Time Meeting Transcription with the Webex JavaScript SDK
canonical_url: https://developer.webex.com/blog/how-to-receive-real-time-meeting-transcription-with-the-webex-javascript-sdk
content_type: blog
date: '2022-02-25'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/how-to-receive-real-time-meeting-transcription-with-the-webex-javascript-sdk)

Phil Bellanti wrote an awesome [blog](https://developer.webex.com/blog/webex-javascript-sdk-now-has-real-time-meeting-transcription) about all the new AI features Webex offers and the recent introduction of real time meeting transcription in our Webex JavaScript SDK. In this follow up blog, I’m going to show you how to build a simple Webex JavaScript SDK application, that will display the real-time transcription content in your console terminal. Step-by-step, I will introduce you to some of the Webex JavaScript SDK basics, but if you are new to Webex programmability, you can always continue your learning journey at https://developer.webex.com.
### Sample App

I also have a small sample application written in vanilla JavaScript. In this application, we initialize the SDK as a Webex user, connect to our cloud, and join a meeting. Assuming Webex Assistant is already turned-on, the application will simply listen for transcription-related events, and inject the received payload inside the text-area of a DOM element. The full source code for this app is available on [GitHub](https://github.com/WXSD-Sales/Sample-App-Transcription).

### The Code

Please note, before the SDK instance JOINS the meeting, Webex Assistant must be turned on. This can be achieved either by manually turning it on through the Meeting Client or programmatically through a new attribute called `enabledWebexAssistantByDefault` of the [/meetingsPreferences](https://developer.webex.com/docs/api/v1/meeting-preferences) API (Setting this parameter to `true` will turn-on Webex Assistant (by default) for all future meetings the user hosts).

Now let's take a look at the code:

Initialize the `webex` instance -- more about [access_token](https://developer.webex.com/docs/getting-started).

```javascript
import Webex from 'webex';

const webex = Webex.init({
  config: {
    credentials: {
      access_token: <YOUR_ACCESS_TOKEN>
    }
  }
});
```

Register the device with Webex Meeting Cloud and sync your meetings with existing meetings on the server.

```javascript
webex.meetings.register()
  .then(() => webex.meetings.syncMeetings())
  .then(() => { /** Registered and Synced up! **/ });
```

Create a meeting with a given destination. This will return a promise to an active meeting object.

```javascript
webex.meetings.create(destination))
  // Save meeting
  .then((meeting) => {
    activeMeeting = meeting;
});
```

Bind the events to receive payloads of transcription data when started and stopped. These events listeners will be bound to the meeting object.

```javascript
function bindMeetingEvents(meeting) {
  meeting.on('meeting:receiveTranscription:started', (payload) => {
    console.log(payload);
  });

  meeting.on('meeting:receiveTranscription:stopped', () => {
    console.log("Not Receiving transcription anymore!")
  });

  meeting.on('error', (err) => {
    console.error(err);
  });
}
```
  
Here is what the payload data structure looks like:

```javascript
/**
  * 
  * id - string                      Transcription payload Unique ID
  * personID - string                Active speaker ID
  * transcription - string           Transcription Context
  * timestamp - string               Time
  * type - string                    Final Or Interim
  * 
  **/
```

Finally, join the meeting and set the flag to receive the transcription payloads.

```javascript
meeting.join({receiveTranscription: true}).then(() => {
    // Joined Successfully!
  });
``` 

There you have it! You should now be able to see the transcription payload data inside your terminal console.

### Getting Help

As always, we have a lot of great developer resources to assist along the way, whether it is needing help leveraging transcriptions in the SDK, or questions about any of the other Webex APIs:

- The official GitHub repo for the Webex JavaScript SDK has documentation for enabling and handling transcriptions -  [https://webex.github.io/webex-js-sdk/api/#transcription](https://webex.github.io/webex-js-sdk/api/#transcription)
- More helpful information on the Webex Assistant feature: [https://help.webex.com/en-US/article/n5eooo0/Use-Webex-Assistant-in-Webex-Meetings-and-Events](https://help.webex.com/en-US/article/n5eooo0/Use-Webex-Assistant-in-Webex-Meetings-and-Events)
- Our amazing Webex Developer Support are available at all hours to help you with questions and for troubleshooting - [https://developer.webex.com/support](https://developer.webex.com/support)
- Feel free to post questions (and answers!) in our new [Webex Developer Community](https://community.cisco.com/t5/webex-for-developers/bd-p/disc-webex-developers)
- For questions about the sample app, please feel free to reach us at wxsd@external.cisco.com.
