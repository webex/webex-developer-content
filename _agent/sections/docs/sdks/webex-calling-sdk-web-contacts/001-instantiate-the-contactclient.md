---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-contacts
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Instantiate the ContactClient
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-contacts). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-contacts.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Calling SDK consists of various modules which are created at the time of its initialization. Among these integral modules, one noteworthy component is the `ContactClient`.

---

For an introduction, we recommend consulting our [Quickstart guide](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) which will walk you through the step-by-step process of creating a calling instance and provide insights into the instantiation of various modules.

By the end of this article, you will have a solid grasp of how to leverage `ContactClient` to enhance your application's calling capabilities and create a seamless user experience.

## Selected section

## Instantiate the ContactClient

The `ContactsClient` is implemented as the `ContactsClient` class in the SDK and there are two ways of instantiating it.

To instantiate just the `ContactsClient`, use the `createContactsClient` method:

```javascript
const contacts = createContactsClient(webex, logger);
```

If the `ContactsClient` is initialized through the `calling` instantiation:

```javascript
const contacts = calling.contactClient;
```
