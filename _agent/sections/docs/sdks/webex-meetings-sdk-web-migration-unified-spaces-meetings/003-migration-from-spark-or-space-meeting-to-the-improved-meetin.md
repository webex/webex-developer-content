---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Migration from Spark or Space meeting to the improved meetings experience
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Limitations](011-limitations.md)

## Article introduction

This guide provides an overview of the improved meeting experience associated with spaces and outlines the impacted areas, along with the necessary adjustments in these areas for the adoption of these improved flows. 

## Selected section

## Migration from Spark or Space meeting to the improved meetings experience

The initial stage of transitioning from Space or Spark (hereafter referred to as the classic meeting experience) to the improved meeting experience involves the management of user licenses as the host's license now determines the meeting capabilities.

- Create a [Webex site](https://help.webex.com/en-us/article/naqlzeu/Add-and-manage-a-Webex-site-in-Control-Hub) and re-distribute the licenses among users.
- Create a [Service App](https://developer.webex.com/docs/service-apps) for end-to-end provisioning of users and other features.



> **Info**
>
> As part of the improved experience with space meetings, creating a guest user through [Guest Issuer](https://developer.webex.com/docs/guest-issuer) is being deprecated. Now the way to create a guest user would be through a [Service App](https://developer.webex.com/docs/service-apps) tied to a guest site.



Users with a Webex account can acquire their access token from the [developer portal](https://developer.webex.com/docs/getting-started) by logging in with their authentication details (username and password).

For guest users, an access token can be obtained via a [Service App](https://developer.webex.com/docs/service-apps).
