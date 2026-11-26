---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-contact-center
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- REST
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-contact-center). [Full Markdown](../../../../docs/webex-contact-center.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

## REST

Many of the Webex Customer Experience APIs are RESTful. Each resource is represented by a base URL such as /agents, and you can view the resources under **API Reference** on the left navigation pane. The available methods are listed under each resource. For instance, navigating to **Agents** displays a method GET /agents/statistics. Clicking the method link takes you to a page that fully details the Agent Statistics API.

Within the details of an API, a **Try Out** capability is available to test calling the endpoint. Here you will provide an access token, and any values (if required) in the form of query parameters, path parameters, or the request body. For endpoints which accept query parameters, path parameters or request bodies, the required parameters (if any) are marked with an asterisk (\*). For responses, the APIs currently support return data in the application/JSON format only. Clicking the copy icon in the request box copies the cURL statement, and any values provided to test the API using **Try Out** are filled into the cURL statement.
