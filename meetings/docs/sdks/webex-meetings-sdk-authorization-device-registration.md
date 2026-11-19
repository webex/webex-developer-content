---
type: Guide
title: Web Meetings SDK | Authorization and Device Registration
display_title: Authorization
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-authorization-device-registration
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-meetings-sdk-authorization-device-registration)

Authorization and device registration are important first steps in starting a meeting using the Web SDK. This document helps in using SDK for authenticating a user and registering the device with the Webex Meetings servers.

## Initialize the SDK

To use the SDK, you'll need a free Webex account; if you don't have a Cisco Webex account, visit [Cisco Webex for Developers](https://developer.webex.com/) to create your account and retrieve your **access token** from [Getting and Using your Personal Access Token](https://developer.webex.com/docs/getting-your-personal-access-token).

To create a new Webex instance:

```js
const webex = Webex.init({
    credentials: {  
       access_token: `<AUTHORIZATION/BOT TOKEN>`
    }
});
```

At this point, the Webex `Meetings` object is ready for use. The `Meetings` object contains a list of meetings as well as methods to perform specific operations or listen for certain events. Detailed information is included in this article.

For more information on the `Meetings` object, see the [Webex Meetings Quickstart](https://developer.webex.com/meeting/docs/sdks/webex-meetings-sdk-web-quickstart).


## Retrieve a Meeting Object

The `Meetings` object is accessible from the `Webex` object:

```js
const webex = new Webex.init();
const meetings = webex.meetings;
```

The `meetings` constant contains an instance of the Webex `Meetings` object.

## Register a Meeting Device

Once the `Meetings` object is instantiated, you can register a device using its `register()` method:

```js
const webex = new Webex.init();
await webex.meetings.register();
```



|              |                        |
| ------------ | ---------------------- |
| Asynchronous | Yes                    |
| Parameters   | No parameters required |
| Returns      | Promise\<undefined\>   |

## Deregister a Meeting Device

You can deregister a registered device using the `Meetings` object's `unregister()` method:

```js
await webex.meetings.unregister();
```

## Meetings Ready Event

A `ready` event fires when a `Meetings` object is ready for use. A `Meetings` object instance is ready once the containing `Webex` object is ready, and all the `Meetings` object's instance parameters are set. You can subscribe to the ready event immediately following `Webex.init`:

```js
webex.meetings.on('meetings:ready',() => {
 console.log('Meetings object is ready for device registration');
 // Register a new device...
});
```

The ready event returns no payload.



> **Info**
>
> Make any Meetings object method calls only after receiving this event.



## Meetings Registered Event

The `registered` event is emitted by a Meetings object after you call the  `register()` method:

```js
webex.meetings.on('meetings:registered',() => {
 console.log('Meetings object is ready to perform other operations');
 // Perform meeting operations like create, sync, etc.
});
```
