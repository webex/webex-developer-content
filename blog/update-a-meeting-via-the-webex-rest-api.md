---
type: Article
title: Update A Meeting via the Webex REST API
canonical_url: https://developer.webex.com/blog/update-a-meeting-via-the-webex-rest-api
content_type: blog
date: '2022-07-13'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/update-a-meeting-via-the-webex-rest-api)

Aww CRUD! You put down the wrong meeting time when planning tomorrow’s stakeholder call! Well, that’s an easy fix when you’re using the Webex client application! But what about one of the many bots, embedded apps, and integrations that use the Webex API? Can they easily update a Webex Meeting’s information?

The answer: YES!

### Repo

The Webex Developer Evangelism Team maintains an organization on GitHub.com full of samples to get you started [here](https://github.com/WebexSamples).

Today, we’ll shout out another one of our [Webex REST API Samples](https://github.com/WebexSamples/rest-api-samples), specifically one that demonstrates a Node.js implementation of making an HTTP PUT request to the API and the example response body. This sample is intended to give hackers who need to programmatically update meeting information using Node a working sample that can be tweaked to update any of the possible properties.

Source code for this walk-through is available here: https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/update .

### TL;DR

Here’s a video where I explain these concepts and demonstrate them in action via our Developer Portal.


	<iframe src="https://app.vidcast.io/share/embed/cc70342d-a7d1-4e36-9eb0-052c9ed50fc3" width="100%" height="100%" title="Update a Meeting with Webex Meetings API!" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>


&nbsp;

### Get Started

This blog is meant to be a supplementary conversation to our API documentation on this topic, available [here](https://developer.webex.com/docs/api/v1/meetings/update-a-meeting) in our Webex Developer Portal. If this is your first introduction to using the Webex REST API’s meetings endpoint, it’s a good idea to check out our [Create a Meeting via the Webex API in Node](https://developer.webex.com/blog/create-a-meeting-in-node-with-the-webex-rest-api) blog post, which serves as an excellent introduction to the topic. Otherwise, keep reading to get a taste of updating meeting details on the fly

#### Modify and Run the Sample Code

The first step is to get the entire update repo into your favorite code editor or online I.D.E. Once you do, you will look out for three (3) lines in the `update_meeting.js` file that look like this:

```javascript
const myWebexDeveloperToken = 'REPLACE WITH API KEY';
const meetingID = 'REPLACE WITH MEETING ID';
const meetingPassword = 'REPLACE WITH MEETING PASSWORD';
```

Your `myWebexDeveloperToken` will come from the Webex Developer Portal mentioned above. The easiest way to get a `meetingID` and `meetingPassword `to play with is by running either the [Create a Meeting](https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/create) or [Read a Meeting](https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/read) code samples from our GitHub. That way, you’ll have a good sample of some of the properties available to be changed in a meeting’s metadata. You can see an example of the shape of this data in the file entitled `example_response.json.`

### But wait…There’s More!

The three variable declarations mentioned above will serve as our authentication and authorization to access this protected data via the Webex REST API. Now, we’ll have to fill in the HTTP request body with some details that will replace any pre-existing data with matching fields. This will be directly below the previous step in the same file and look something like this:

```javascript
const body = JSON.stringify({
    title: 'The Power of the Webex REST API!', agenda: 'This meeting will share the awesome technical achievement that is Webex REST API.',
    password: meetingPassword,
    start: '2022-06-19T19:00:00Z’,
    end:   '2022-06-19T21:00:00Z'
});
```

As you can see, our `meetingPassword` gets passed into the body of the of the request along with any parameters that need to be updated. A full list of meeting object parameters is available on the Webex Developer Portal.

#### Request

If you’ve gotten this far, our sample will do the rest of the magic for you! We package up our request options within an HTTP request, and then tack on the request body, all using Node’s built-in ‘http’ module.

#### Response

The expected response for a successful HTTP PUT request to the Webex REST API meetings endpoint will be a single meeting object nested within an array. This object will be the current version of this meeting’s metadata after your update. This should be accompanied by a 200 HTTP Status Code.
For an example of what this response should look like, visit our GitHub repository covering this material [here](https://github.com/WebexSamples/rest-api-samples/blob/main/meetings/update/example_response.json).

### Dive Deeper

Webex’s team of Developer Evangelists is devoted not only to showing off all the powerful solutions that can be built using the Webex platform, but also to helping you along the journey to achieve them for your organization’s project. This sample is only a teaser to get your feet wet. Jump in the deep end when you check out our [Webex Developer Portal](https://developer.webex.com/) to learn about what’s possible. Once you do, come tread water in our [Developer Community](https://community.cisco.com/t5/webex-for-developers/bd-p/disc-webex-developers) to get support on your project and share what you’re building!

### Hack On!

What's next? Join the conversation on the Webex for Developers Community Forum: [https://cs.co/WebexDeveloperCommunity](https://cs.co/WebexDeveloperCommunity). Need help? The [Webex Developer Support Team](https://developer.webex.com/support) is standing by! Comments? Requests? Tweet us [@WebexDevs](https://twitter.com/WebexDevs), or [open an issue](https://github.com/WebexSamples/rest-api-samples/issues) on GitHub. This blog covers the "U" in CRUD. You can also check out Webex REST API meetings code samples for [Create](https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/create), [Read](https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/read), and [Delete](https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/delete).
