---
type: Excerpt
canonical_url: https://developer.webex.com/blog/meet-webex-node-webex-javascript-sdk-built-for-node-js
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- A First Node.js Script
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/meet-webex-node-webex-javascript-sdk-built-for-node-js). [Full Markdown](../../../../blog/meet-webex-node-webex-javascript-sdk-built-for-node-js.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The [`webex-node`](https://www.npmjs.com/package/webex-node) package gives server-side JavaScript a supported Webex SDK entry point for Messaging, automation, bots, command-line tools, and backend services without loading browser-only media components.

---

## Selected section

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
