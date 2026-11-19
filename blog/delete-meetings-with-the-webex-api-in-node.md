---
type: Article
title: Delete Meetings with the Webex API in Node
canonical_url: https://developer.webex.com/blog/delete-meetings-with-the-webex-api-in-node
content_type: blog
date: '2022-07-19'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/delete-meetings-with-the-webex-api-in-node)

There are recently published blogs and sample code about implementing the CRUD (Create, Read, Update, Delete) process with the Webex RESTful API, minus the `Delete` process. In this follow up blog, I’m going to show you how to delete a meeting programmatically. If you are new to the Webex RESTful API, you can always continue learning at [https://developer.webex.com/](https://developer.webex.com/).

### Webex Rest API Samples

The Webex Meetings Rest API enables seamless integration of Webex Meetings into your websites and apps. You can schedule meetings, send meeting invitations, list meetings, and more. The full source code for this sample project is available on [GitHub](https://github.com/WebexSamples/rest-api-samples). You can also find many more samples/examples in the repository that is managed by the Webex Developer Evangelist team [here](https://github.com/WebexSamples).

### Using the Sample Code

Before getting started with setting up the project, you are going to need to replace the generic `String` values (lines 34 and 35 in `delete_meeting.js`) stored in the variables shown in the below portion of code with the bearer token associated with your Webex developer account, and the meeting ID that resolves to the meeting intended to be deleted.

```javascript
const myWebexDeveloperToken = 'REPLACE ME WITH YOUR WEBEX DEVELOPER PERSONAL ACCESS TOKEN';
const meetingId = 'REPLACE WITH MEETING ID';
```

You can use the **Try It Now** feature for a quick way to acquire a meeting ID without having to write any code on the [List Meetings](https://developer.webex.com/docs/api/v1/meetings/list-meetings) API endpoint if you are logged into the Webex Developer portal.

Once set up is completed, you can follow the instructions in the projects `README` file and run the below command from a CLI.

```bash
node ./delete_meeting.js
```

Upon a successful execution of the sample code, you should receive a `204 (No Content)` status code as there is no further information supplied in the response body.

### Try It Now

A copy of the sample code is available on GitHub:

[https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/delete](https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/delete)

### Engage with Us

The [Webex Developer Community](https://community.cisco.com/t5/webex-for-developers/welcome-to-the-webex-for-developers-forum/m-p/4558386#M321) has dedicated topics, discussion groups, and announcements. Also, follow [Webex Devs](https://twitter.com/webexdevs?lang=en) on Twitter. We encourage you to tell us about your experience using the above sample code.
