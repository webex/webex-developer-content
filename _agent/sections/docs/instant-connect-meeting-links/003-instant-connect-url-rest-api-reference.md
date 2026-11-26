---
type: Excerpt
canonical_url: https://developer.webex.com/docs/instant-connect-meeting-links
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Instant Connect URL REST API Reference
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/instant-connect-meeting-links). [Full Markdown](../../../../docs/instant-connect-meeting-links.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

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

## Selected section

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
