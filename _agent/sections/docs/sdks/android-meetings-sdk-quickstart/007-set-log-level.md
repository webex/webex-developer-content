---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-quickstart
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Set Log Level
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides examples of common API usage within the meetings flow. For detailed API information, please refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/android-sdk-overview#sdk-api-reference).

---

The `Webex` instance serves as the primary entry point for the SDK, providing access to all Webex SDK APIs. The `Call` object represents a meeting and offers APIs for actions such as joining, leaving, muting, and unmuting. The `Call` object is returned as a result of a successful `dial` API call.

## Selected section

## Set Log Level

To adjust the log level for debugging purposes:

```kotlin
webex.setLogLevel(logLevel: LogLevel)
```
