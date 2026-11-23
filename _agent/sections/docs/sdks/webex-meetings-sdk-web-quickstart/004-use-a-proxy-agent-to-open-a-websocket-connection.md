---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-quickstart
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Use a Proxy Agent to Open a WebSocket Connection
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-quickstart). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Meetings SDK. This guide is designed to provide developers with a concise walkthrough to swiftly set up, authorize, and test the core meeting functionalities within the Meeting SDK. 

---

By following the sequential flow of this document and integrating the provided code snippets, you'll be able to authenticate your application and create and manage your first meetings. Whether you're new to Webex's Meeting SDK or looking to brush up on the basics, this guide ensures a streamlined experience to get you up and running in no time. Let's dive in!

## Selected section

## Use a Proxy Agent to Open a WebSocket Connection

For consumers who are not using the SDK via the browser, it may be necessary to configure a proxy agent to connect with Mercury and open a WebSocket in a proxy environment. This can be done by configuring an agent as part of a `DefaultMercuryOptions` config object. The agent object will then be injected into the SDK and used in the Mercury plug-in during WebSocket construction as an option property, allowing a connection to be established via the specified proxy URL:

```js
const webex = require(`webex`);
const HttpsProxyAgent = require('https-proxy-agent');

let httpsProxyAgent = new HttpsProxyAgent(url.parse(proxyUrl));

webex.init({
  config: {
    defaultMercuryOptions: {
      agent: httpsProxyAgent
    }
  }
});
```
