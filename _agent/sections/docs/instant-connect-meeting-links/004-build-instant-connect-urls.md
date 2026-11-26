---
type: Excerpt
canonical_url: https://developer.webex.com/docs/instant-connect-meeting-links
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Build Instant Connect URLs
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/instant-connect-meeting-links). [Full Markdown](../../../../docs/instant-connect-meeting-links.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This guide shows how you can construct Instant Connect URLs for hosts and guests.

---

Using a simple REST API, you can easily generate Instant Connect URLs for one or multiple hosts and guests. The API allows for a variety of customizations via its request payload, including:

- A configurable meeting subject
- Not before and expiration times for the authorization JWT
- Device support
- Parameters to set the number of hosts and guests up to a maximum of 25 each
- An option to generate short URLs
- Various advanced encryption options

The guide includes a step by step example using Postman, if you're new to REST APIs. Alternatively, if you're a REST veteran, you can skip directly to the API Reference materials at the end of this document.

## Selected section

## Build Instant Connect URLs

Depending upon whether you've generated regular or "short" URLs you can build final Instant Connect URLs in one of two ways.

### Build Long URLs

The following URLs are used as bases for the complete host and guest URLs. The API generates a cipher which you then append to the `&data=` portion of the base URL:

- **Host**: `https://instant.webex.com/gen/v1/login?int=jose&v=1&data=`
- **Guest**: `https://instant.webex.com/gen/v1/talk?int=jose&v=1&data=` 

Append your API response `cipher` values as the `&data=` parameter value to form your Webex Instant Connect meeting for host and guest long URLs.

#### Long URL Examples

- **Host URL**:`https://instant.webex.com/gen/v1/login?int=jose&v=1&data=eyJwMnMiOiJfRFN ... ufUvar_w` 
- **Guest URL**:`https://instant.webex.com/gen/v1/talk?int=jose&v=1&data=eyJwMnMiOiJYZVp ... dL_GqSw`

### Build Short URLs

To construct a final short URL, append the `short` key values to the `baseUrl` generated in the response.

#### Short URL Examples

- **Host URL**: `https://instant.webex.com/visit/m8iHTzH`
- **Guest URL**: `https://instant.webex.com/visit/oJCP7UY`
