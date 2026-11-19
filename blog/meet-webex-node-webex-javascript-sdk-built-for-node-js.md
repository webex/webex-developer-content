---
type: Article
title: 'Meet webex-node: The Webex JavaScript SDK Built for Node.js'
canonical_url: https://developer.webex.com/blog/meet-webex-node-webex-javascript-sdk-built-for-node-js
content_type: blog
date: '2026-07-10'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/meet-webex-node-webex-javascript-sdk-built-for-node-js)

The [`webex-node`](https://www.npmjs.com/package/webex-node) package gives server-side JavaScript a supported Webex SDK entry point for Messaging, automation, bots, command-line tools, and backend services without loading browser-only media components.

---

## Why a Node.js-Specific Package?

For years, the [`webex`](https://www.npmjs.com/package/webex) npm package has given JavaScript developers a convenient way to add Webex capabilities to an application. It remains the right choice for browser experiences—including applications that use Webex Meetings, Calling, or Contact Center.

But a browser and a Node.js process are very different environments. A browser supplies APIs such as `window` and the media stack needed for real-time audio and video. A command-line script, automation worker, or backend service does not. Beginning with version 3 of the SDK, importing the full `webex` package directly into Node.js could load browser-dependent media components and fail with a `window is not defined` error.

That is the gap [`webex-node`](https://www.npmjs.com/package/webex-node) was created to fill.

Released in April 2025 and now documented on the [Webex for Developers Node.js SDK page](https://developer.webex.com/messaging/docs/sdks/node), `webex-node` provides a supported Webex JavaScript SDK entry point designed specifically for a Node.js runtime. It preserves the familiar SDK programming model for Messaging and related Webex APIs while leaving out browser-only media components.

## One SDK Family, Two Runtime-Focused Packages

Both packages come from the same [`webex-js-sdk`](https://github.com/webex/webex-js-sdk) project and share the same core concepts. In either environment, developers initialize a Webex client and work with APIs such as rooms, messages, memberships, people, teams, and webhooks.

The important difference is what each package loads and where it is intended to run.

| Choose | When your application runs in | Best suited for |
| --- | --- | --- |
| `webex-node` | Node.js, without a browser DOM | CLI tools, scheduled jobs, automation, bots, webhook services, and backend integrations using Messaging and related REST-backed APIs |
| `webex` | A web browser or browser-bundled application | Interactive web experiences, especially those using Meetings, Calling, Contact Center, or other browser media capabilities |

The full `webex` package includes media-oriented dependencies for Meetings, Calling, and Contact Center. Those capabilities rely on browser facilities and are intentionally excluded from `webex-node`. The result is not a second, unrelated SDK. It is a Node-focused distribution of the same SDK family with a runtime-appropriate capability boundary.

That boundary is also the principal limitation to remember: `webex-node` cannot be used for Meetings, Calling, or Contact Center media flows. If an application needs to join a meeting, place a call, or handle media in the browser, use `webex` and the appropriate browser SDK documentation.

## What Is webex-node Good For?

The package is a natural fit anywhere Webex work should happen without a visible browser interface.

### Command-Line Utilities

A developer can build a terminal command that creates a project space, posts release notes, looks up a person, or adds members to a space. This is useful for internal tooling and repeatable operational workflows where opening a web page would only add friction.

### CI/CD and Scheduled Automation

A Node.js job can post deployment results to a Webex space, create a collaboration space for a new project, or send a daily report. The same approach works in a CI pipeline, a cron job, a container, or a serverless function with a supported Node.js runtime.

### Backend Integrations

An Express, Fastify, or other Node.js service can use `webex-node` to connect application events with Webex. For example, a service could receive a business event, format a notification, and post it to the appropriate space. It can also create and manage Webex webhooks as part of an integration.

### Messaging Bots and Workflow Services

For a bot or workflow that needs direct SDK access, `webex-node` provides the underlying Messaging APIs without pulling browser media modules into the process. A production bot will still need an inbound-event design—typically Webex webhooks delivered to a publicly reachable endpoint—but its outbound Webex operations can use the SDK's rooms, messages, memberships, and related APIs.

### Administrative and Migration Scripts

One-off scripts are often the fastest way to perform a controlled bulk task: inspect spaces, reconcile memberships, or move a repeatable API procedure into source control. `webex-node` lets Node.js developers do that through SDK methods instead of assembling every HTTP request by hand.

## A First Node.js Script

The current getting-started guide calls for Node.js 20 and npm 10. Create a project and install the package:

```bash
mkdir webex-node-hello
cd webex-node-hello
npm init -y
npm install webex-node
```

Add `"type": "module"` to `package.json`, then create `index.js`:

```js
import WebexNode from 'webex-node';

const webex = WebexNode.init({
  credentials: {
    access_token: process.env.WEBEX_ACCESS_TOKEN,
  },
});

webex.once('ready', async () => {
  try {
    if (!webex.canAuthorize) {
      throw new Error('Webex authorization failed');
    }

    const room = await webex.rooms.create({
      title: 'Hello from Node.js',
    });

    await webex.messages.create({
      roomId: room.id,
      markdown: '**Hello from `webex-node`!**',
    });

    console.log(`Created space: ${room.title}`);
  } catch (error) {
    console.error(error);
    process.exitCode = 1;
  }
});
```

Set a token in the environment and run the script:

```bash
WEBEX_ACCESS_TOKEN='<your-token>' node index.js
```

For a quick local test, a personal access token can help validate the flow. Personal access tokens are short-lived and intended for development only. For a production workload, use the authentication model appropriate to the application—such as a Webex bot or an OAuth integration—and keep credentials out of source code.

When troubleshooting, the SDK also supports log-level control through the environment. For example:

```bash
WEBEX_LOG_LEVEL=debug WEBEX_ACCESS_TOKEN='<your-token>' node index.js
```

## How to Choose

The simplest decision rule is to choose by runtime and required capability:

- If the code runs as a Node.js process and needs Messaging or related management APIs, start with `webex-node`.
- If the code runs in a browser and needs a user-facing Webex experience, use `webex`.
- If the application needs Meetings, Calling, or Contact Center media flows, use `webex`; those capabilities are outside the scope of `webex-node`.
- If the solution has both a browser frontend and a Node.js backend, it can use both packages—each on its own side of the application boundary.

That last pattern is often the most useful. A browser can own the interactive experience and real-time media, while a backend safely performs scheduled work, responds to webhooks, and integrates Webex with other systems.

## A Clearer Path for Server-Side JavaScript

`webex-node` does not introduce a separate set of Webex APIs. Its most important capability is simpler and more practical: it gives server-side JavaScript a supported package boundary that matches the Node.js runtime.

For developers building terminal tools, automation, bots, and backend services, that means no browser shim, no accidental dependency on `window`, and no need to load media capabilities the application will never use. Install the package, initialize the familiar Webex client, and put Webex Messaging to work wherever Node.js runs.

To get started, visit the [Webex Node.js SDK documentation](https://developer.webex.com/messaging/docs/sdks/node) or explore the [`webex-node` source and README](https://github.com/webex/webex-js-sdk/tree/next/packages/webex-node).
