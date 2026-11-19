---
type: Excerpt
canonical_url: https://developer.webex.com/docs/ea-tips-tricks-test
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Checking for an Existing Sharing Session
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/ea-tips-tricks-test). [Full Markdown](../../../../docs/ea-tips-tricks-test.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

**[Embedded Apps Guide](https://developer.webex.com/docs/ea-developer-guide-test) > Workflow**
* * * 

## Selected section

## Checking for an Existing Sharing Session

It's good practice to check the value of [`app.isShared`](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+isShared) before calling `setShareUrl()`. This avoids the scenario of the "Open together" button mistakenly appearing for meeting participants.

For example, in the following code sample the embedded app's `handleSetShare()` is responsible for calling `setShareUrl()` in response to some other event. The function first checks the value of `app.isShared` and exits the function if it's `true`.

```javascript
function handleSetShare(url)
    if (app.isShared) {
      log('ERROR: setShareUrl() should not be called while session is active');
      return;
    }
    // Call setShareUrl() as usual...
}
```

<a id="check-if-meeting-or-space"></a>
