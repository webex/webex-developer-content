---
type: Excerpt
canonical_url: https://developer.webex.com/docs/ea-tips-tricks-test
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Using Cookies and Web Storage
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/ea-tips-tricks-test). [Full Markdown](../../../../docs/ea-tips-tricks-test.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

**[Embedded Apps Guide](https://developer.webex.com/docs/ea-developer-guide-test) > Workflow**
* * * 

## Selected section

## Using Cookies and Web Storage

Embedded apps can use [cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies) and [Web Storage](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API) the same way they are used in web browsers. Persistent cookies and local storage data are persisted after a user quits the Webex app or Meeting Center client; session cookies and session storage data are deleted when the user closes Webex or Meeting Center.

The [Webex Kitchen Sink app](https://github.com/WebexSamples/EmbeddedAppSample) on GitHub demonstrates the various storage options.

![Screenshot of storage options](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt97007cc6cddd1122/local-storage-options.png)

<a id="integrations"></a>
