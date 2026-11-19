---
type: Guide
title: Web Calling SDK | Authorization and Device Registration
display_title: Authorization
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-authorization-device-registration
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-calling-sdk-authorization-device-registration)

Authorization and device creation are crucial initial steps in leveraging the full capabilities of the calling SDK. Authorization ensures secure access and permissions for developers, while device creation establishes the necessary endpoint for enabling voice and video communication features in your application.

## Obtain an Access Token

Developers can obtain an access token by leveraging Common Identity, which employs the OAuth 2.0 authorization framework for secure and standardized token-based authentication. To get up and running with the OAuth 2.0 flow, you can refer [to this detailed guide](https://developer.webex.com/docs/login-with-webex) which runs through the necessary steps, including user consent and redirection, to generate a short-lived authorization code.

After receiving the authorization code, you can use the `curl` utility with the following example API call to exchange it for an access token:

```bash
curl -X POST https://webexapis.com/v1/access_token \
  -d "grant_type=authorization_code" \
  -d "client_id=YOUR_CLIENT_ID" \
  -d "client_secret=YOUR_CLIENT_SECRET" \
  -d "code=AUTHORIZATION_CODE" \
  -d "redirect_uri=YOUR_REDIRECT_URI"
```

Once you obtain the access token, it acts as the credential for secure API interactions with various Webex services, including the `CallingClient` module. The developer.webex.com website serves as a comprehensive resource throughout this OAuth 2.0 process, enabling you to seamlessly integrate Webex features into your application while mitigating security concerns.



> **Info**
>
> To authorize with Webex Calling, a developer must select the appropriate scopes while creating the Integration, or pass these scopes if directly creating an access token. [Scopes](https://developer.webex.com/docs/integrations#scopes) define the level of access that an integration requires. Webex Calling requires these scopes: `spark:webrtc_calling`, `spark:calls_read`, `spark:calls_write`, and `spark:xsi`.



## Authorize with Webex Calling

Registering an endpoint with Webex Calling is a pivotal step in authorizing a user to access voice and video communication features. Once a user is provisioned in an organization licensed for Webex Calling, the `CallingClient` module can be used to initiate the registration process. That involves obtaining an access token via OAuth 2.0 authentication. Upon successful authentication, the `CallingClient` module registers the endpoint, thereby enabling it to place and receive calls through the Webex cloud. Once registration is complete, the SDK automatically sends requests at regular intervals to maintain the endpoint's active registration status.

Additional details regarding the registration process can be found below.

### Obtaining a Line Object

A line object is created at the time of the `callingClient` initialization itself. It can be obtained by fetching the list of all the lines using `getLines` method in the callingClient module. However, the SDK only supports a single line at the moment.

For example:

```js
const callingClient  = calling.callingClient;
const lines = callingClient.getLines();
```

The constant, `lines`, is an object where the keys are the `lineId` of each line and the values are the line Objects themselves.



> **Info**
>
> Please refer to [the getting started documentation](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) for information on the creation and initialization of the `Calling` object. The example above is just pseudocode indicating that `callingClient` is a part of the main `calling` object).



Each of the line objects contain the following information:



|**Properties**|**Description**|**Type**|
| --- | --- | --- |
| `lineId` | Unique ID provisioned per line in order to distinguish and identify them within the application. |`string<uuid>` |
| `mobiusDeviceId` | Unique ID provisioned per line for communication between the SDK and the backend. |`string<uuid>` |
| `phoneNumber` | External phone number for the line. | `string` |
| `extension` |  Internal extension for the line. | `string` |
| `status` | Registration status of the line (initially set to inactive). | `string` |
| `sipAddresses` | Address provided by Webex Calling when the line is registered. | `string\[\]` |
| `voicemail` | Voicemail Pilot number for each line. | `string` |
| `lastSeen` | Last interaction of the line with Webex Calling. | `string` |
| `keepaliveInterval`   | Time interval after which the registration for a line expires. | `number` | 
| `callKeepaliveInterval` |  Interval within which the Calling SDK needs to send a ping to keep the call alive on Webex Calling. |`number` |
| `rehomingIntervalMin` |  The minimum interval for the Line to return to the primary Webex Calling server. |`number` |
| `rehomingIntervalMax` | The maximum interval for the Line to return to the primary Webex Calling server. | `number` |
| `voicePortalNumber` | Reserved for Webex Contact Center. | `number` |
| `voicePortalExtension` | Reserved for the Webex Contact Center. | `number` |

## Register a Device

The line object can be used to perform various line operations including device registration. The device registration process can be begun by using the `line` object's `register()' method:

```js
line.register();
```



| **Asynchronous** | No |
| --- | --- |
| **Parameters** | No parameters required |
| **Returns** | undefined |



> **Info**
>
> The `register()` method only begins the registration process. It does not mean the registration is complete.



### Determine if Registration is Successful

The `register` method only begins the registration process. To verify that the device registration is successful, register a callback to listen for the `registered` event:

```js
line.on('registered', (line: ILine) => {
    // Store the line registration details
}
```

With the help of the `registered` event, you'll know the both that the registration has completed sucessfully and also have access to the `line` detials. 



> **Info**
>
> The event subscription must happen before making the `register()` call.



## Deregister a Device

You can derigister a registered device using the `line` object's `deregister()` method:

```js
line.deregister();
```



| **Asynchronous** | No |
| --- | --- |
| **Parameters** | No parameters required |
| **Returns** | undefined |



> **Info**
>
> The `deregister()` method only begins the registration process. It does not mean that deregistration is complete.




### Determine if Deregistration is Successful

The `deregister` method only begins the registration process. To verify that the device registration is successful, register a callback to listen for the `unregistered` event:

```js
line.on('unregistered', () => {
    // Add any action that should happen after a line is unregistered
}
```



> **Info**
>
> The event subscription must happen before making the `deregister()` call.



## The Connecting Event

By listening for the `connecting` event,  the app can determine that it's in the connecting state once the `register()` call is made: 

```js
line.on('connecting', () => {
    // Store the line registration details
}
```

This event has no payload. If the event listener is triggered, it means the line is connecting.

## The Error Event

By listening for the `error` event, the app can monitor any errors encountered during the registration process:

```js
line.on('error', (error) => {
    // Try to re-connect and/or show error to end user
}
```

This event returns an `error` payload. If this event listener is triggered, it means the line connection encountered one of the following errors:



| **Status** | **Type** | **Message** |
| --- | --- | --- |
| `inactive` | `registrationError` | Device limit exceeded. The user already logged in to a different device. |
| `inactive` | `registrationError` | Device not found. |
| `inactive` | `tokenError` | Token expired. Authentication/Authorization error. |

 An example error object is returned in JSON:

```json
{
 "status": "inactive",
 "type": "tokenError",
 "msg": "Token expired. Authentication/Authorization error."
}
```
