---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/browser
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/browser). [Full Markdown](../../../../../docs/sdks/browser.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Getting Started](003-getting-started.md) [Limitations](007-limitations.md)

## Article introduction

Add Webex products and features to your web apps with the Webex Browser SDK.

[GitHub](<https://github.com/webex/webex-js-sdk>)
[NPM](<https://www.npmjs.com/package/webex>)

## Selected section

## Troubleshooting

If you're having trouble with the Browser SDK, here's some more information to help troubleshoot the issue.

### SDK Requirements

Review the following SDK requirements to make sure you're using the correct minimum versions of Node.js, npm, etc.:

- [Node.js](https://nodejs.org/) LTS 16.x and later
- [npm](https://www.npmjs.com/) 6.x and later
- Optionally: [nvm](https://github.com/creationix/nvm/) to manage Node.js versions
- Supported Desktop Browsers: Chrome (latest), Firefox (latest), and Safari (latest)
- Supported Mobile Browsers: Chrome for Android and Safari for iOS
- A Webex account and an integration with the necessary [scopes](https://developer.webex.com/docs/integrations#scopes)

**Note:**

- If you are joining a meeting with a browser on an Android 12 device (Pixel or other Android devices, except Samsung), the remote video could be corrupted. This issue is fixed in Google Chrome v97 (https://chromereleases.googleblog.com/). Please upgrade to this version.
- If you are using the BrowserSDK to join a meeting with Safari on an iPhone with iOS 15.1, you may experience an issue after calling `addMedia()` to join the meeting. This has been traced to a [known webRTC bug](https://bugs.webkit.org/show_bug.cgi?id=232490) with Safari on iOS 15.1. This issue has been fixed in iOS 15.2, so upgrading to 15.2 should fix the issue.

### Additional Logging

You can add additional logging to your application to help narrow down any issues with the SDK.

#### Change the Log Level Within Your App

When you initialize the JavaScript SDK, you can set the log level to `info` to see more logging to help troubleshoot the issue:

```javascript
const webex = window.Webex.init({
  credentials: {
    access_token: myAccessToken
  },
  logger: {
    level: 'info'
  }
});

```

To see even more logging, set the log level to `debug`.

### Firewall Ports

The Browser SDK makes use of several network protocols and ports. If you're encountering connection or connectivity issues, make sure there aren't any firewalls blocking or preventing communication with any Webex endpoints. For more information about the network and web security requirements for Webex services, please see [Network Requirements for Webex Services](https://help.webex.com/WBX000028782/).

### Getting Support

If you're stumped, contact the [Webex Developer Support team](https://developer.webex.com/support) for more help with the SDK.
