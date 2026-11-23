---
type: Excerpt
canonical_url: https://developer.webex.com/docs/instant-connect-meeting-links
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Step by Step Instant Connect API Call Using Postman
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
