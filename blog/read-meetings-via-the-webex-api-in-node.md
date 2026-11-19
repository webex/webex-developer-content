---
type: Article
title: Read Meetings via the Webex API in Node
canonical_url: https://developer.webex.com/blog/read-meetings-via-the-webex-api-in-node
content_type: blog
date: '2022-07-06'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/read-meetings-via-the-webex-api-in-node)

Today we’ll talk about code that demonstrates how easy it is to get started using the Webex REST APIs meeting endpoints. This lets us quickly get a list of an authenticated user’s meetings. Do you have an idea for a scheduling app that needs access to a user’s Webex Meetings? This sample will help you create a solution in Node.js that allows you to automate interactions with the API on behalf of a user. 

### Video

**TL;DR?** Here is a video from our Webex Meetings API series covering this material:


<iframe src="https://app.vidcast.io/share/embed/6f664de0-85ff-4935-a5a7-acb2eecdc4b3" width="100%" height="100%" title="Read Meetings from Webex Meetings API!" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>

&nbsp;

### Repo

The Webex Developer Evangelism Team maintains an organization on GitHub.com: [https://github.com/WebexSamples](https://github.com/WebexSamples). There, you’ll find several repositories with sample code for a quick start, and examples of implementation. You can find source code for today’s discussion here:[https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/read](https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/read).

### Get Started

If you’re not already familiar with our Webex for Developers portal, you’ll want to check that out here: [https://www.developer.webex.com/](https://www.developer.webex.com/). [Create a Meeting via the Webex API in Node](https://developer.webex.com/blog/create-a-meeting-in-node-with-the-webex-rest-api) is the first installment in this CRUD series. Look there for an introduction to getting an Authorization token from the portal and using it to get a response back from the API. Those are prerequisites to what we’re doing here. In fact, you’ll want to create a meeting first, so you’ll have something to read.

### Modify and Run the Sample Code

Now that you’re familiar with this paradigm, it’s easy to clone the Github repository, plug in your token from our Webex for Developers portal, and get a response from our API. It’s also possible to use any of the online IDEs to copy, replace and request. You’ll look for a line in the JavaScript file that looks like this:

```javascript
const myWebexDeveloperToken = 'REPLACE ME WITH YOUR WEBEX DEVELOPER PERSONAL ACCESS TOKEN';
```

### Now What?

Now that you can interact with the meetings API, the possibilities are endless! This easy sample shows how to properly send a request using Node.js and gives an example of the response object.

#### Request

This sample sends a request to the Webex API’s meeting endpoint with your Authorization token in the request header. Developers also have the option to pass more information to the API to specify what meetings they want. If the `roomId` parameter is included in the request, the API will only return meetings from the specified room. Or if we want our response to only include specific types of meetings, then we can include the `meetingType` parameter and set its value to `meetingSeries`, `scheduledMeeting` , or `meeting`.

Look below at the options object, which our request method will use to determine the URL, HTTP request type, and to pass our authorization token. This is also where we would include additional parameters.

```javascript
const options = {
  method: ‘GET’,
  hostname: ‘webexapis.com’,
  path: ‘/vi/meetings’,
  port: 443,
  headers: {
    Authorization: `Bearer ${myWebexDeveloperToken}`, //Make sure you set your token above!
  },
};
```

#### Response

Without passing any other options to the request body, the expected response to our sample request is a list of meetings on the user’s calendar, sorted chronologically. A quick glance over the response object reveals how rich the metadata for each meeting object is. In our sample, we take this list and print a message to the console that tells us the title of the user’s next meeting, which is the first item in this list. Below is an example of this response, with only one meeting returned for simplicity.

```javascript
{
  “items”: [
    {
      "id": "870f51ff287b41be84648412901e0402_I_167427437874906709",
      "meetingSeriesId": "870f51ff287b41be84648412901e0402",
      "scheduledMeetingId": "870f51ff287b41be84648412901e0402_20191101T120000Z",
      "title": "Example Daily Meeting",
      "agenda": "Example Agenda",
      "meetingType": "meeting",
      "state": "ended",
      "excludePassword": false,
      "publicMeeting": false,
      "enableAutomaticLock": false,
      "timezone": "UTC",
      "start": "2019-11-01T12:12:15Z",
      "end": "2019-11-01T12:51:33Z",
      "hostUserId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9jN2ZkNzNmMi05ZjFlLTQ3ZjctYWEwNS05ZWI5OGJiNjljYzY",
      "hostDisplayName": "John Andersen",
      "hostEmail": "john.andersen@example.com",
      "siteUrl": "site4-example.webex.com",
      "webLink": "https://site4-example.webex.com/site4/j.php?MTID=870f51ff287b41be84648412901e0402_I_167427437874906709",
      "integrationTags": [
            "dbaeceebea5c4a63ac9d5ef1edfe36b9",
            "85e1d6319aa94c0583a6891280e3437d",
            "27226d1311b947f3a68d6bdf8e4e19a1"
        ]
    }
  ]
}
```

### Take the Baton

Now that you know how simple it is to send a `READ` request and get a response back from Webex REST API, your next objective will be to learn about `PUT` requests to the meetings endpoint. *Update a Meeting via Webex REST API* will be the next article in this series and will put you one step closer to having full “CRUD” capabilities!

### Hack On!

What's next? Join the conversation on the Webex for Developers Community Forum: [https://cs.co/WebexDeveloperCommunity](https://cs.co/WebexDeveloperCommunity). Need help? The [Webex Developer Support Team](https://developer.webex.com/support) is standing by! Comments? Requests? Tweet us [@WebexDevs](https://twitter.com/WebexDevs), or [open an issue](https://github.com/WebexSamples/rest-api-samples/issues) on GitHub. This blog covers the "R" in CRUD. You can also check out Webex REST API meetings code samples for [Create](https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/create), [Update](https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/update), and [Delete](https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/delete).
