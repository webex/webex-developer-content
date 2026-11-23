---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-voicemail
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Initialize the voicemailClient
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-voicemail). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-voicemail.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `VoicemailClient` object is a supplementary Calling SDK module that adds comprehensive support for voicemail functionality. 

---

Before continuing, refer to the [Quickstart Guide](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) to understand how `Call` objects are created and how different modules are instantiated. The `VoicemailClient` object offers a variety of functions which are covered in this article in detail.

## Selected section

## Initialize the voicemailClient

The `VoicemailClient` is implemented as the `Voicemail` class in the SDK and there are two ways of instantiating it.

To instantiate just the `VoicemailClient`, use the `createVoicemailClient` method:

```javascript
const voicemailClient = createVoicemailClient(webex, logger);
```

If the `VoicemailClient` is instantiated through the `calling` instantiation:

```javascript
const voicemailClient = calling.voicemailClient;
```

The voicemail client instance must be initialized to enable access to the voicemail backend services using the `init()` methood of the `voicemailClient` object:

```javascript
const initResponse = await voicemailClient.init();
```
