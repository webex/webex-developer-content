---
type: Article
title: Create a Meeting in Node with the Webex REST API
canonical_url: https://developer.webex.com/blog/create-a-meeting-in-node-with-the-webex-rest-api
content_type: blog
date: '2022-06-27'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/create-a-meeting-in-node-with-the-webex-rest-api)

As an end user, we can create meetings in the Webex app. They magically go up into the servers that operate behind the scenes, and we don't think twice about it. But what happens when we want to write software that can do the same thing? A Webex "[integration](https://developer.webex.com/docs/integrations)" is one example of a software solution that can do this.

There are several ways to interact with Webex. Today, we're going to go on a journey into creating meetings via the Webex API. That means Application Programming Interface. There are lots of kinds of APIs. Webex has offered XML APIs for a while now, but those are being phased out. Modern software has essentially centralized around the HTTP (HyperText Transfer) protocol, using a standard we refer to as "REST". That means Representational State Transfer. So the idea is that we utilize this standard to exchange information. You want to send a few things to Webex: proof that you're an authorized app; proof that the user you're helping wants your help; and, of course, the actual instructions you want to send to take the desired effect. In today's sample code, we're going to look at sending the instructions to create a new Webex meeting.

Alright, that's a lot of moving pieces. We'll break this down into the smallest digestible units for this exploration, so we can focus on just the elements we want to learn today.

So, on a good day, we'd be building a full solution. We'd use OAuth to authenticate our users, and our code would act upon their behalf. But hey, as Developers, it's kind of nice to get to square one in a hurry. We'll be taking that shortcut today, so stay tuned for the differences to follow.

### Video

TL;DR? Here is Aaron walking you through the process:

	<iframe src="https://app.vidcast.io/share/embed/231f5242-623d-4d9c-a5a9-a3295f6fc853" width="100%" height="100%" title="Create a Meeting with Webex Meetings API!" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>


&nbsp;

### Code Repository

The Webex Developer Evangelism Team maintains an organization on GitHub.com:

https://github.com/WebexSamples

On this organization, we've got several repos with code samples and examples.

We'll be working in this one today: https://github.com/WebexSamples/rest-api-samples

Let's look at some code samples for the basic CRUD (Create Read Update Delete) interactions with the Webex REST API as pertains to meetings. This installment will explore the first part: Create. Be sure to check out the other three!

https://github.com/WebexSamples/rest-api-samples/tree/main/meetings

As you read across this CRUD series, keep in mind some actions require others to be completed first. The meeting you create in this installment can be the one you access to read, update, and then delete in the subsequent installments. It makes sense to go through them in this order:

- https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/create
- https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/read
- https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/update
- https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/delete

&nbsp;

### Run the Request in Your Browser Right in the Docs

The Webex Developer documentation is alive! You can actually run REST API calls from within your browser window, right inside the docs. This is great when you want to use a quick tool to call the API, but we're actually going to be writing some code, so we'll need a token to authenticate from our development machine. If you don't already have a Webex account, go ahead and sign up! You'll need an account to use the APIs and SDKs.

### Get a Token
When making requests to the Webex REST API, an Authentication HTTP header is used to identify the requesting user. This header must include an access token. This access token may be a personal access token from this site (see below), a Bot token, or an OAuth token from an Integration or Guest Issuer application.

Our interactive API Reference uses your personal access token, which can be used to interact with the Webex API as yourself. This token has a short lifetime—only 12 hours after logging into this site—so it shouldn't be used outside of app development. When using this token, any actions taken through the API will be done as you.

Visit https://developer.webex.com/docs/getting-started and scroll down to "Your Personal Access Token". You'll copy this, paste it into the sample code file you want to run, save, and send it in your REST client requests as a bearer token in the headers.

### Modify and Run the Sample Code

The first thing you will need to do to try this code sample is to change it! To do that, you'll need a copy that you can edit. The quickest way to get one is to clone a copy of the repo from GitHub down to your development machine. You could also download a zip archive of the repository, decompress it, and navigate to the file we'll be running:

https://github.com/WebexSamples/rest-api-samples/blob/main/meetings/create/create_meeting.js

Read the comment block at the top of the file for detailed, step-by-step instructions. Your goal: replace the line that says

`const myWebexDeveloperToken = 'REPLACE ME WITH YOUR WEBEX DEVELOPER PERSONAL ACCESS TOKEN';`

with your token in place of the placeholder text. You *could* also edit the parameters for the meeting we'll be creating. After all, it's going to be added to your account. Make it whatever title, start, and end that you'd like to create. The default example is fine, but take note of the date in case you're reading this way before or way after the hard coded date in the example. You might have trouble locating it if the date is too far in the future. You should update it to something at least a little in the future if you're running this after the example date has passed.

The rest of the code is wired up so you don't have to touch it, but it's worth a read. We make a barebones HTTPS request; no libraries, no frameworks. From within the `meetings/create/` directory, where the `create_meeting.js` file lives, we're going to run the following command in the terminal:

`node ./create_meeting.js`

A successful response will be JSON that looks like this:

https://github.com/WebexSamples/rest-api-samples/blob/main/meetings/create/example_response.json

### What's Going On?

Alright, it's all well and good to see the thing successfully run, but what is actually happening when it runs?

#### Request
The first thing that happens is that a TLS-secured HTTP request (HTTPS) is sent from your development machine to the Webex API Endpoint. These requests must be properly-formed HTTP calls, such as GET, POST, UPDATE, and DELETE. In this case, we want to create a meeting, so we use POST. How do we know to do that? Why, the docs, of course!

Starting from https://developer.webex.com/docs/platform-introduction on the Webex Developer Documentation, we scroll down the left-hand navigation to the *APIs* section.

Under *Webex APIs* we see *+ Meetings*; click that to expand. We see *Overview*, *+ Guides*, and the one we want: *+ Reference*. As you can see, there are several endpoints to explore. The one we're working with is simply titled *Meetings*. Clicking that brings us to our goal:

https://developer.webex.com/docs/api/v1/meetings

See the table with *Method* and *Description*? That first entry, described as "Create a Meeting", has an icon left of the endpoint that says, yup, "POST".

#### Response

What should we expect to get back? JSON! As shown above, there's an example_response.json file in the repo to reference for details. When you run the code, the response JSON is being parsed and displayed in the terminal. You can also view a response using the interactive docs page. Click on that URL for the Meetings Create endpoint and you'll land here:

https://developer.webex.com/docs/api/v1/meetings/create-a-meeting

Be sure you're logged in to use this functionality! The developer.webex.com site will automatically put your 12-hour token into the browser for you, and you can view the response right there as you run it!

### Making a Real-World Project

Alright, now that we've established the quick-and-dirty way to learn and test creating a meeting via the Webex REST API, how would you go about taking that knowledge into a real-world project? Well, first and foremost, you'll stop using the temporary personal access token you used to try this code sample, and will instead create an access token to be used by your app. You'd wire up that app to handle an OAuth flow allowing your app users to give permission for your code to run on their behalf.

You'd probably want to use a library or framework to provide you with easy functionality, scalable project scope, and nice things like error handling, logging, etc. At the core, you'll know what's happening under the hood! You've manually created a meeting in your Webex account using the Webex REST API with a few lines of JavaScript running on your localhost with Node!

### Hack On!

What's next? Join the conversation on the Webex for Developers Community Forum: https://cs.co/WebexDeveloperCommunity

Need help? The [Webex Developer Support Team](https://developer.webex.com/support) is standing by!

Comments? Requests? Tweet us [@WebexDevs](https://twitter.com/WebexDevs), or [open an issue](https://github.com/WebexSamples/rest-api-samples/issues) on GitHub.

This blog covers the "C" in CRUD. You can also check out Webex REST API meetings code samples for [Read](https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/read), [Update](https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/update), and [Delete](https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/delete).
