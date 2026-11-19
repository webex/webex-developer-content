---
type: Guide
title: Instant Connect Meeting Links
display_title: Instant Connect Meeting Links
canonical_url: https://developer.webex.com/docs/instant-connect-meeting-links
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/instant-connect-meeting-links)

This guide shows how you can construct Instant Connect URLs for hosts and guests.

---

Using a simple REST API, you can easily generate Instant Connect URLs for one or multiple hosts and guests. The API allows for a variety of customizations via its request payload, including:

- A configurable meeting subject
- Not before and expiration times for the authorization JWT
- Device support
- Parameters to set the number of hosts and guests up to a maximum of 25 each
- An option to generate short URLs
- Various advanced encryption options

The guide includes a step by step example using Postman, if you're new to REST APIs. Alternatively, if you're a REST veteran, you can skip directly to the API Reference materials at the end of this document.

## Prerequisites

Before you can use Instant Connect, your Webex Admin will need to login to the Instant Connect webpage and choose **Activate Instant Connect** here:<https://instant.webex.com/integrate/>.



> **Info**
>
> You only have to activate Instant Connect once.



Next, you'll need to generate an access token which is required to make the API call to retrieve the encrypted part of the URLs. You've got two options for access tokens:

- A 12 hour time limited Personal Access token for development purposes
- A 100 year Bot token for production use

In addition, optionally, to enable adding devices to the meeting, you'll need to configure Instant Rounding as described in the following help.webex.com article [Configure Virtual Rounding](https://help.webex.com/article/6vsdoi/).

### Retrieve a Personal Access Token for Development

To obtain a Webex Personal Access Token (valid for 12 hours), navigate to the [Webex Developer Portal](https://developer.webex.com/docs/getting-started#accounts-and-authentication), login with your Webex org admin account, and copy the Bearer token value:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt84e562902cf23694/63c03de3d2d671109381b574/01-personal-token.png)

### Retrieve a Bot Token for Production Usage

For a production-level implementation, we recommend [creating a new Webex Bot](https://developer.webex.com/my-apps/new/bot) and using the Bot’s access token (valid for 100 years). You can copy the Bot access token once you've created your new bot:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8125b962e4bdceda/63c03de3def66d1d64a3b768/02-bot-token.png)

## Step by Step Instant Connect API Call Using Postman

With your access token, you use the Instant Connect API to retrieve the encrypted ciphers that you'll append to the base URLs for hosts and guests. In this section we'll use [Postman](https://www.postman.com/) to walk you through an example REST call that generates ciphers for a single host and a single participant using the minimum required request payload.

**NOTE**: This example uses the desktop version of Postman, but the web version works just as well.

To retrieve the encrypted ciphers using Postman:

1. Open Postman and select **New**.

    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt73a64c78866daa17/63c03de398b11c3ccecf6e19/03-postman-new.png)

1. Choose **Environment**.

    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte1f7779d5e14df7d/63c03de33daf00107c0b94e5/04-postman-new-environment.png)

1. Name your new environment, in this case *InstantConnect* and define the two following variables with the corresponding values:

    - **Name**: `mtg-broker-url`; **Value**: `https://mtg-broker-a.wbx2.com`
    - **Name**: `bot-token`; **Value**: your personal access token or bot token

    Click **Save**.

    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt793604859f72b3ed/63c03de3d2737e13210ed51b/05-postman-environment-setup.png)

1. Choose your new environment from the drop down list.

    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5f73960f8ff190f4/63c03de3a0db4d3e821f024e/06-postman-choose-environment.png)

1. Choose **New**.

    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte2e8cc2c3e78ea84/63c03de3bf8ad51208627dc1/07-postman-new-request.png)

1. Choose **HTTP Request**.

    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt73f44f7b080f4b31/63c03de33ae0f31fad3f52d7/08-postman-HTTP-request.png)

1. Configure the request as follows:
    - Choose **POST** as the request type.
    - Enter `{{mtg-broker-url}}/api/v2/joseencrypt` as the URL.
    - Select **Auth**, choose **Bearer Token** as the **Type**, and enter `{{bot-token}}` as the value for the token.

    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltecfa05ea6f7c8018/63c03de35d2483134881cb7c/09-postman-HTTP-request-config-1.png)

1. Select **Body**, select the type as **raw JSON** and enter the following JSON string (you can change the `sub` (subject) string to whatever you'd like):

    ```json
    {
      "jwt": {
      "sub": "Subject goes here."
      },
      "aud": "a4d886b0-979f-4e2c-a958-3e8c14605e51"
    }
    ```

    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltfa3b884ff82961e0/63c03de399e03c1edceda614/10-postman-HTTP-request-config-2.png)

1. Select **Send**. You'll see the response in the **Body** tab of the Postman console.

    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt0427f97ba16254c9/63c03deff4a590109efb8aef/11-postman-HTTP-response.png)

Your response will look something like:

```json
{
    "host": [
        {
            "cipher": "eyJwMnMiOiJiLVZB...-xtzA"
        }
    ],
    "guest": [
        {
            "cipher": "eyJwMnMiOiJuNmxv...FaqA"
        }
    ]
}
```

You'll notice you've got two `cipher` values, one for the host and one for a single guest. Those are the values that you'll append to the meeting URL after `&data=`.



> **Info**
>
> The `cipher` values are truncated to save space.



For the host URL after appending the cipher, you'll get:

`https://instant.webex.com/gen/v1/login?int=jose&v=1&data=eyJwMnMiOiJiLVZB...-xtzA`

For the guest URL after appending the cipher, you'll get:

`https://instant.webex.com/gen/v1/talk?int=jose&v=1&data=eyJwMnMiOiJuNmxv...FaqA`

The remaining sections describe additional configurations and contain complete reference materials.

## Instant Connect URL REST API Reference

This section contains the full reference for all of the Instant Connect URL REST API including example requests and responses.

### Request Endpoint

The REST API endpoint is:

- `POST https://mtg-broker-a.wbx2.com/api/v2/joseencrypt`

### Request Headers

Use the following headers in your request:

- **Content-Type**: `application/json`
- **Authorization**: `Bearer <Personal or Bot access token goes here>`

### Body Parameters

Use the following body parameters to customize your REST request:



| Parameter | Description |
| --- | --- |
| `aud` (**required**) | String<br />Value: `a4d886b0-979f-4e2c-a958-3e8c14605e51`<br />Indicates the audience for which the JWT is intended. |
| `jwt` (**required**) | Object |
| `sub` (**required**) (under `jwt`) | String<br />A unique value in your organization which will be used to place hosts and guests into the same collaboration space. |
| `nbf` (under `jwt`) | Integer<br />The `nbf` (not before) claim identifies the time given as the number of seconds from the Unix Epoch (`1970-01-01T00:00:00Z UTC`) before which the JWT will not be accepted for processing. |
| `exp` (under `jwt`) | Integer<br />The `exp` (expiration time) claim identifies the expiration time given as the number of seconds from the Unix Epoch (`1970-01-01T00:00:00Z UTC`) on or after which the JWT will not be accepted for processing. If not specified, set for 15 minutes later than the time when the request was made. |
| `flow` | Object |
| `id` (under `flow`) | String<br />Takes only one value currently - `sip-no-knock`. If `id` is defined along with data mentioned below, the SIP addresses mentioned in the data object will be called to join the Instant Connect Meeting. |
| `data` (under `flow`) | Object<br />List of Cisco Device SIP addresses that should be added to this meeting automatically. |
| `numHost` | Integer [0 … 25]<br />Default: `1`<br />Number of encrypted strings to be used by hosts. <br />**NOTE**: The maximum number of links, combining both host and guest, that can be requested at one time is 25. |
| `numGuest` | Integer [0 … 25]<br />Default: `1`<br />Number of encrypted strings to be used by guests. <br />**NOTE**: The maximum number of links, combining both host and guest, that can be requested at one time is 25. |
| `provideShortUrls` | Boolean<br />Default: `false`<br />If set to `true`, the response will have shortened data portions of the meeting URL. It will also contain a shortened base URL |
| `verticalType` | String<br />Default: `hc`<br />Relevant only if `provideShortUrls` is `true`. Currently takes two values, `gen` (for general flow) and `hc` (for healthcare flow). |
| `loginUrlForHost` | Boolean<br />Default: `true`<br />Relevant only if `provideShortUrls` is true. If set to `false`, the short URL for hosts will be non-login links which means the host won't have an option to login for the meeting. |
| `jweAlg` | String<br />Default: `PBES2-HS512+A256KW`<br />Enum: `PBES2-HS256+A128KW PBES2-HS384+A192KW PBES2-HS512+A256KW` <br />Algorithm to encrypt the Content Encryption Key, which produces the JWE Encrypted Key. |
| `saltLength` | Integer [8 … 128]<br />Default: Random value between `8` and `128` inclusive.<br />Length of the salt to be used in conjunction with `jweAlg`. |
| `iterations` | Integer [1000 … 32767]<br />Default: A random value between `1000` and `32767` inclusive.<br />Number of iterations to be used in conjunction with the `jweAlg`. |
| `enc` | String<br />Default: `A256GCM`<br />Options: `A128CBC-HS256 A192CBC-HS384 A256CBC-HS512 A128GCM A192GCM A256GCM`<br />Algorithm used to encrypt the JWT. |
| `jwsAlg` | String<br />Default: `HS512`<br />Options: `HS256 HS384 HS512`<br />Algorithm used to sign the JWT. |

### Response

A successful request returns:

- A response message of type `200 OK`

- A response payload of type`application/json`


### Request and Response Payload Examples

The following examples show various request payloads as a formatting reference as well as their resultant responses.



> **Info**
>
> The `cipher` values are truncated to save space.



#### Minimum Request Body Payload

```json
{
  "jwt": {
    "sub": "Subject goes here."
  },
  "aud": "a4d886b0-979f-4e2c-a958-3e8c14605e51"
}
```

#### Response from the Minimal Request Body

```json
{
    "host": [
        {
            "cipher": "eyJwMnMiOiJiLVZB...-xtzA"
        }
    ],
    "guest": [
        {
            "cipher": "eyJwMnMiOiJuNmxv...FaqA"
        }
    ]
}
```

#### Complete Sample JSON Request Payload Without Device Support

To create multiple host and guest URLs in the same response, increase the value of `numHost` and `numGuest` up to a maximum of 25.

```json
{
  "jwt": {
    "sub": "Subject goes here.",
    "Nbf": 1671480433000,
    "Exp": 1671480433000
  },
  "aud": "a4d886b0-979f-4e2c-a958-3e8c14605e51",
  "numGuest": 1,
  "numHost": 1,
  "provideShortUrls": false,
  "verticalType": "gen",
  "loginUrlForHost": false,
  "jweAlg": "PBES2-HS512+A256KW",
  "saltLength": 8,
  "iterations": 1000,
  "enc": "A256GCM",
  "jwsAlg": "HS512"
}
```

#### Complete Sample JSON Response Payload Without Device Support 

In this case the response will appear similar to the minimal request payload response above. The cipher provided, however will reflect the additional configuration options. In addition, increasing the values for `numHost` and `numGuest` will return multiple cipher instances that you can use to create multiple Instant Connect URLs.

#### Sample Request Payload Generating Short URLs

Adding the parameter `provideShortUrls` generates short URLs in addition to the regular cipher.

**TIP**: When you use the `provideShortUrls` parameter, you can also specify the `loginUrlForHost` parameter which, when set to `false`, disables login for the host.

```json
{
  "jwt": {
    "sub": "Subject goes here."
  },
  "aud": "a4d886b0-979f-4e2c-a958-3e8c14605e51",
  "provideShortUrls": true
}
```

#### Short URL Response Payload

The `short` values are combined with the `baseUrl` value in the response payload to generate "short" URLs as described below. The `cipher` values can be used as described below as well.

```json
{
    "host": [
        {
            "cipher": "eyJwMnMiOiJQUnJX ... EbZaQ",
            "short": "Kuyqdx3"
        }
    ],
    "guest": [
        {
            "cipher": "eyJwMnMiOiJPamRX ... xVfyA",
            "short": "LCFCNRz"
        }
    ],
    "baseUrl": "https://instant.webex.com/visit/"
}
```

#### Complete Sample JSON Request Payload Including Device Support

To enable device support, add the `flow` element to the `jwt` element in your regular request body.

```json
{
  "jwt": {
    "sub": "Subject goes here.",
    "Nbf": 1671480433000,
    "Exp": 1671480433000,
    "flow": {
      "id": "sip-no-knock",
      "data": [
        {
          "uri": "instant_rounding@intadmin.room.wbx2.com"
        }
      ]
    }
  },
  "aud": "a4d886b0-979f-4e2c-a958-3e8c14605e51",
  "numGuest": 1,
  "numHost": 1,
  "provideShortUrls": true,
  "verticalType": "gen",
  "loginUrlForHost": false,
  "jweAlg": "PBES2-HS512+A256KW",
  "saltLength": 8,
  "iterations": 1000,
  "enc": "A256GCM",
  "jwsAlg": "HS512"
}
```

#### Complete Sample JSON Response Payload Including Device Support 

As with the other complete payload, the response will appear similar to the minimal request payload response above. The cipher provided, however will reflect the additional configuration options.

## Build Instant Connect URLs

Depending upon whether you've generated regular or "short" URLs you can build final Instant Connect URLs in one of two ways.

### Build Long URLs

The following URLs are used as bases for the complete host and guest URLs. The API generates a cipher which you then append to the `&data=` portion of the base URL:

- **Host**: `https://instant.webex.com/gen/v1/login?int=jose&v=1&data=`
- **Guest**: `https://instant.webex.com/gen/v1/talk?int=jose&v=1&data=` 

Append your API response `cipher` values as the `&data=` parameter value to form your Webex Instant Connect meeting for host and guest long URLs.

#### Long URL Examples

- **Host URL**:`https://instant.webex.com/gen/v1/login?int=jose&v=1&data=eyJwMnMiOiJfRFN ... ufUvar_w` 
- **Guest URL**:`https://instant.webex.com/gen/v1/talk?int=jose&v=1&data=eyJwMnMiOiJYZVp ... dL_GqSw`

### Build Short URLs

To construct a final short URL, append the `short` key values to the `baseUrl` generated in the response.

#### Short URL Examples

- **Host URL**: `https://instant.webex.com/visit/m8iHTzH`
- **Guest URL**: `https://instant.webex.com/visit/oJCP7UY`
