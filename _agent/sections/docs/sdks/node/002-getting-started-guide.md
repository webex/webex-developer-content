---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/node
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Getting Started Guide
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/node). [Full Markdown](../../../../../docs/sdks/node.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Add Webex products and features to your web apps with the Webex Node.js SDK.

[GitHub](<https://github.com/webex/webex-js-sdk/tree/next/packages/webex-node>)
[NPM](<https://www.npmjs.com/package/webex-node>)

## Selected section

## Getting Started Guide

In this example, we'll use Node.js to create a simple project that will post a message to a room.



> **Info**
>
> If you're interested in integrating Webex functionality in your front-end web applications, check out the [Browser SDK](https://developer.webex.com/docs/sdks/browser).



### Overview

* Create a Webex space
* Post a Message

### Requirements

* [Node.js](https://nodejs.org/) 20, [npm](https://www.npmjs.com/) 10.x
* Optionally: [nvm](https://github.com/creationix/nvm/) to manage Node.js versions

### Limitations

* The `webex-node` package cannot be used for Meetings, Calling and Contact Center flows.

### Step 1: Create the Project Directory

```bash
cd /my/project/directory
npm init
```

You’ll be prompted to answer a few simple questions, but typically the defaults are just fine.

### Step 2: Install the JavaScript SDK

Now, install `webex-node`:

```bash
npm install --save webex-node
```
```bash
yarn add webex-node
```

### Step 3: Start Using the SDK

So, you want to send a message. For demonstration purposes, we’ll use environment variables to authorize the SDK with your personal access token. If you're logged into this site, you can find your token in [Getting Started](https://developer.webex.com/docs/getting-started). This token provides access to your account for testing purposes, and shouldn't be used for anything other than testing. If you don't already have a Webex account, click Sign Up at the top of this page to create a new account.

Use the `@webex/test-webex-node` package in the webex-js-sdk repository as a guide to using the `webex-node` package. Refer to the [README](https://github.com/webex/webex-js-sdk/tree/next/packages/%40webex/test-webex-node) for more information.

Here is a snippet of code that can be used.
```javascript
import WebexNode from 'webex-node';

const webex = WebexNode.init({
  credentials: {
    access_token: 'INSERT TOKEN HERE',
  },
});

webex.once('ready', () => {
  if (webex.canAuthorize) {
    // eslint-disable-next-line no-console
    console.log('webex is authorized');
    webex.rooms
      .create({
        title: 'Test Space from NodeJS',
      })
      .then(function (room) {
        // eslint-disable-next-line no-console
        console.log('room object', room);
        webex.messages.create({
          text: 'Hello World!',
          roomId: room.id,
        });
      })
      // Make sure to log errors in case something goes wrong.
      .catch(function (reason) {
        console.error(reason);
        process.exit(1);
      });
  }
});
```

Run the above script using the `node` command. The script will use your token to create a space called "Test Space from NodeJS" and send a message in that space.
