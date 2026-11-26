---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/node
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting the Node.js SDK
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/node). [Full Markdown](../../../../../docs/sdks/node.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Getting Started Guide](002-getting-started-guide.md)

## Article introduction

Add Webex products and features to your web apps with the Webex Node.js SDK.

[GitHub](<https://github.com/webex/webex-js-sdk/tree/next/packages/webex-node>)
[NPM](<https://www.npmjs.com/package/webex-node>)

## Selected section

## Troubleshooting the Node.js SDK

If you're having trouble with the Node.js SDK, here's some more information to help troubleshoot the issue.

### SDK Requirements

Review the following SDK requirements to make sure you're using the correct minimum versions of Node.js, npm, etc.:

* [Node.js](https://nodejs.org/) LTS 20.x
* [npm](https://www.npmjs.com/) 10.x
* Optionally: [nvm](https://github.com/creationix/nvm/) to manage Node.js versions
* A Webex account and an integration with the necessary [scopes](https://developer.webex.com/docs/integrations#scopes)

### Additional Logging

You can add additional logging to your application to help narrow down any issues with the SDK.

#### Change the Log Level via an Environment Variable

You can change the log level via the `WEBEX_LOG_LEVEL` environment variable. For example, if you start your application server via `npm serve`, you'd set the variable before running your application to see increased logging:

```bash
WEBEX_LOG_LEVEL=info npm serve
```

While developing your application, you can set the `WEBEX_LOG_LEVEL` environment variable to `debug` see even more logging. For example, if you start your application server via `npm serve-dev`, you'd set the variable before running your application to see increased logging:

```bash
WEBEX_LOG_LEVEL=debug npm serve-dev
```

### Firewall Ports

The Node.js SDK makes use of several network protocols and ports. If you're encountering connection or connectivity issues, make sure there aren't any firewalls blocking or preventing communication with any Webex endpoints. For more information about the network and web security requirements for Webex services, please see [Network Requirements for Webex Services](https://help.webex.com/WBX000028782/).
