---
type: Article
title: Accessing Real-Time Webex Meeting Media via the Webex Browser SDK
canonical_url: https://developer.webex.com/blog/how-to-build-meeting-bots-for-webex
content_type: blog
date: '2023-05-08'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/how-to-build-meeting-bots-for-webex)

> **Warning**
>
> Editor's Note: In this guest column by our development partner, Recall.ai, they have shown how they have opened a brand-new method of combining guest issuer and the Webex Browser SDK to enable media access to an integration! **This is a Third-Party API implementation. And has not been tested by Cisco.**



Our conversation data holds a wealth of valuable information. Recent advancements in AI enable new products to be built on top of the audio and video from meetings. Some examples include:

- Sales tools that create follow up emails from the content of the sales meeting
- Education tools that provide live captions for hard-of-hearing students
- Hiring tools that prompt the interviewer with relevant follow up questions to ask during the interview
- Meeting facilitation tools that show the speaker talk times to encourage more equitable meetings 
- User research tools that analyze facial expressions from user interviews

The above use cases require access to meeting data. There are two primary ways to access this data. 

1. Use the Webex RESTful API to pull in cloud recordings.
1. Build a media recording application.

In this blog post we will be focusing on the second option of building a recording app. A recording app is typically used when a developer needs to access real-time data, such as live video streams, audio streams, active speaker events, and more.

### Building the Webex Integration

We will go through the steps to build a Webex meeting recording application. This app will join meetings, record audio and video, and leave the meeting when it's done.

#### Setup Guest Issuer Credentials

<br/>

- Sign up for a developer account on [Webex's developer portal](https://developer.webex.com/).
- Navigate to the **My Webex Apps** section from the top right corner.
- Click on **Create a Guest Issuer** and fill in the relevant details.
- Take note of the **Guest Issuer ID** and **Guest Issuer Secret** as they will be needed in following steps

&nbsp;

#### Install and Authorize the Webex JS SDK

Install the Webex JS SDK in your project with `npm install webex --save`

Initialize the SDK and authorize using a JWT (JSON Web Token). Use the Guest Issuer ID and Secret obtained in earlier step to generate the token. You can use `crypto-js` for encoding the secrets.

```javascript
// Import and initialize 
import { init as initWebex } from "webex";
const webex = initWebex();

// Authorize the SDK
const jwt = buildJwt();
webex.authorization.requestAccessTokenFromJwt({
  jwt,
}).then(() => {
  // SDK authorization has succeeded
});

// Build the JWT
import * as Base64url from "crypto-js/enc-base64url";
import * as Base64 from "crypto-js/enc-base64";
import * as Utf8 from "crypto-js/enc-utf8";
import * as hmacSHA256 from "crypto-js/hmac-sha256";
function buildJwt() {
  const payload = {
    sub: "webex-bot-1",
    name: "My Webex App",
    iss: ADD_YOUR_GUEST_ISSUER_ID_HERE,
      // 1h expiry time
    exp: (Math.floor(new Date().getTime() / 1000) + 60 * 60).toString(),
  };

  const encodedHeader = Base64url.stringify(
    Utf8.parse(JSON.stringify({
      typ: "JWT",
      alg: "HS256",
    }))
  );
  const encodedPayload = Base64url.stringify(
    Utf8.parse(JSON.stringify(payload))
  );
  const encodedData = `${encodedHeader}.${encodedPayload}`;
  const signature = hmacSHA256(
    encodedData,
    Base64.parse(issuer_secret)
  ).toString(Base64url);

  return `${encodedData}.${signature}`;
}
```

#### Join the Meeting

Create a meeting object using the meeting link and join the meeting. Listen to the `self:unlocked` event on the meeting object to know when the app has joined the call.

```javascript
webex.meetings.create(meetingLink).then((meeting) => {
  // Meeting object created successfully|
  // Attach unlock listener
  meeting.on("self:unlocked", () => {
    // The app should be in the call now
  });
  // Trigger join
  meeting.join();
});
```

&nbsp;

#### Get Access to the Meeting Media

Listen to the `media:ready` event on the meeting object to get access to the specific MediaStreams.

```bash
meeting.on("media:ready", ({ type, stream }) => {
  // type can be 'remoteAudio' | 'remoteVideo' | 'remoteShare'
  // Use "stream" to get access to the MediaStream object
});
```

&nbsp;

#### Leave the Meeting

Once we're done, we need to make the app leave the meeting.

```javascript
meeting.leave();
```

We have now built a Webex Meeting Recording Application that will join meetings to access the audio and video streams.

### Recall.ai

If you are looking to build a meeting recording application, but do not want to the burden of running and scaling the infrastructure, [Recall.ai](https://www.recall.ai/) may be a good option. It is a developer-friendly API for meeting bots and applications. By using Recall.ai, you save months of engineering time that you would need to build, scale, and maintain these applications yourself. Instead, you can focus your time on what you do with the meeting data, and not how you get it.

### Conclusion

Meeting recordings are an invaluable data source with numerous product applications. When working with real-time meeting data, building a meeting app is the best way to go about it. However, if you do not have the time or resources to dedicate to creating your own recording app, [Recall.ai](https://www.recall.ai/) can be a useful solution to get to market fast.
