---
type: Excerpt
canonical_url: https://developer.webex.com/docs/ea-handling-events-test
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Events Emitted by the Framework
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/ea-handling-events-test). [Full Markdown](../../../../docs/ea-handling-events-test.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

**[Embedded Apps Guide](https://developer.webex.com/docs/ea-developer-guide-test) > Event Handling**
* * * 

## Selected section

## Events Emitted by the Framework

The following events are emitted by the framework. 

* `application:shareStateChanged` &mdash; when the sharing state of a shared URL changes.

    **Properties**

    | Name | Type | Description |
    | --- | --- | --- |
    | isShared | <code>boolean</code> | Indicates if sharing is taking place. |

* `application:displayContextChanged` &mdash; Emitted when the app's rendering context changes, such as when a user pops out the app from the sidebar into its own window.

    **Properties**

    | Name | Type | Description |
    | --- | --- | --- |
    | displayContext | <code>string</code> | Indicates the new display context. |

* `application:themeChanged` &mdash; Emitted when the user changes the color theme in the Meeting Center or Webex client.

    **Properties**

    | Name | Type | Description |
    | --- | --- | --- |
    | theme | <code>string</code> | Indicates the current theme, LIGHT or DARK. |

* `meeting:infoChanged` &mdash; Emitted when information has changed for the meeting in which the embedded app is running.
* `meeting:roleChanged` &mdash; Emitted when the role for the current participant changes, such as from
* `space:infoChanged` &mdash; Emitted when changes are made to information about the current space, such as the space's title.
