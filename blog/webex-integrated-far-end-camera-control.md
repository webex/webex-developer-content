---
type: Article
title: Webex Integrated Far-End Camera Control
canonical_url: https://developer.webex.com/blog/webex-integrated-far-end-camera-control
content_type: blog
date: '2026-05-05'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-integrated-far-end-camera-control)

Picture a patient room in a hospital, where the patient is meeting with a remote specialist. The camera is on the wall, but the doctor who needs to **frame the shot** to get a better look at an ailment is on Webex at home, or in another building. Far-end camera control (FECC) on the device is not new; what this sample explores is how to put those controls *in the Webex client* so the same person who is already in the meeting can pan, tilt, and zoom without a separate integration.

In this post, we walk through a small proof-of-concept: a bot-backed service that opens a **room tab** in Webex’s embedded browser, serves a simple web UI, and drives [Camera.Ramp](https://roomos.cisco.com/xapi/Command.Camera.Ramp/?search=ramp) on the far-end device through **xAPI**. If you are new to Webex programmability, you can still follow the README links to the REST and xAPI docs you will need.

### What the remote participant sees

The Webex user, perhaps a physician, in the meeting gets a direct message that points them at a Camera Control tab. Inside that tab they see directional controls and sliders.  If they press-and-hold the camera will begin moving in the corresponding direction, and on release movement will stop.  This is the same RoomOS behavior they would get at the codec locally, only rendered as a web page.

### What is happening under the hood

First, a macro on the device recognizes when it has received a call and **POSTs** to this service’s `/call` endpoint with the room device’s serial and a Webex participant identifier (the person who called). The service looks up the device, sends the participant a DM, and creates or replaces the **room tab** whose URL is the public `WEBAPP_PUBLIC_URL`, with `?deviceId=` so the embedded browser loads the right device context.

Second, the web UI talks to `POST /api/fecc/command` on the backend-`rampStart` and `rampStop` with a direction and passes that to the device with [xAPI](https://roomos.cisco.com/xapi/Command.Camera.Ramp/?search=ramp). You are not calling xAPI from the browser directly; the service is the only place that holds that trust boundary.  That way, you can control who has access to the service without exposing sensitive device credentials to the end user.

Third, when the call ends, the same device macro from the beginning hits `/call-end` so the service can tear down and remove the tab.

### How to get started

The full source is on [GitHub](https://github.com/wxsd-sales/webex-integrated-fecc). For API context, see the [getting-started guide](https://developer.webex.com/docs/getting-started) and the [device xAPI docs](https://roomos.cisco.com/xapi).

1. **Give the bot access where it actually matters**\
   Create a [bot](https://developer.webex.com/my-apps/new/bot) and save its token for `WEBEX_BOT_TOKEN`. Then, in **Control Hub**, open the **workspace** that contains the room device (not the device page) and under *Devices* use *Edit API access* to add the bot with **Full access** so it can use the Devices API and xAPI for that workspace. Details [here](https://github.com/wxsd-sales/webex-integrated-fecc?tab=readme-ov-file#setup-bot).
2. **Publish the app with HTTPS**\
   Copy `.env.example` to `.env`, set the bot token, and set `WEBAPP_PUBLIC_URL` to the HTTPS origin where this Node app is reachable, with no trailing slash. Webex loads the tab in a client web view; localhost only works if you tunnel or proxy the same URL you put in the env file. Optional `PORT` defaults to 3000. Details [here](https://github.com/wxsd-sales/webex-integrated-fecc?tab=readme-ov-file#setup-environment).
3. **Load the Macro on the RoomOS device to control**\
   Make a copy of the [macro for the device](https://github.com/wxsd-sales/webex-integrated-fecc/blob/main/macro/integrated-fecc.js) with the camera you want to control remotely.  On line 3, change the `baseUrl` to be the same value as `WEBAPP_PUBLIC_URL`.  After that, you should simply be able to load the macro on your RoomOS device, toggle it on and it will handle the requests to your [backend service](https://github.com/wxsd-sales/webex-integrated-fecc/blob/main/README.md#setup-device-macro).
4. **Run the server**\
   Install and start the server.  The macro takes care of the POSTs to /call and the cleanup routes when calls start and end. Commands [here](https://github.com/wxsd-sales/webex-integrated-fecc?tab=readme-ov-file#install-and-start-locally).

<br/>

### See it in action

For a quick overview of behavior and setup, checkout the [Vidcast](https://app.vidcast.io/share/f936e8ac-14ef-4bd4-bd28-1ddc995a2c73)! 

### In closing

If you are building experiences that combine RoomOS, automation, and the Webex client, this repo is less about the sliders and more about the pattern: REST and xAPI behind a small web UI in a room tab, with a clear split between what runs in the browser and what runs on your server. If you have questions about Webex APIs or SDKs, you can reach developer support at [devsupport@webex.com](mailto:devsupport@webex.com). For questions about this WXSD sales engineering sample specifically, use [wxsd@external.cisco.com](mailto:wxsd@external.cisco.com).
