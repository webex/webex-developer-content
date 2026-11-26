---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-quickstart
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Test Your Application
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-quickstart). [Full Markdown](../../../../docs/cc-web-widgets-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md) [Known Issues/Limitations](010-known-issues-limitations.md)

## Article introduction

This Quickstart Guide walks you through integrating Webex Contact Center capabilities using React widgets into your application from the ground up. Follow these steps to create a fully functional application.

## Selected section

## Test Your Application

1. **Open the application** in your browser (http://localhost:3000)
2. **Enter your access token** in the input field. This can be obtained from the [Developer Portal](https://developer.webex.com). You can log in to the Developer Portal using one of the users from your Contact Center Org account or the test users from the sandbox account.
3. **Use StationLogin** to select your connection type (Desktop/Extension/Dial Number)
4. **Change agent state** using the `UserState` widget to `Available`
5. Make a call to the entry point number from a softphone (you can use the [Webex Web Calling Client](https://web.webex.com/calling?calling)). Here you can log in to the softphone using one of the users from your Contact Center Org account or the test users available in the sandbox account.
6. You should be able to receive the call on the Webex Contact Center Widgets application you created above.

**Congratulations!** 🎉 You now have a fully functional Webex Contact Center Widgets application running from scratch.
