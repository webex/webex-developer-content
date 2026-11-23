---
type: Excerpt
canonical_url: https://developer.webex.com/docs/journey-getting-started
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Technical Details
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/journey-getting-started). [Full Markdown](../../../../docs/journey-getting-started.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Cisco Journey Data Service (CJDS) is a journey management service that helps organizations turn raw customer data into real-time insights and actions. It enables businesses to unify identity, track intent signals, and drive smarter, more personalized interactions through Webex Contact Center.

## Selected section

## Technical Details

### Authentication for CJDS APIs

- CJDS uses Bearer Auth for all APIs. You will need to use CI generated Bearer Token in the 'Authorization' header.
- Prefix token with 'Bearer'. Please look at the [Authentication](https://developer.webex.com/docs/authentication) section on how to generate a bearer token. You can also get the Bearer token from [https://developer.webex.com](https://developer.webex.com/) login with your admin credentials.
- It requires a full administrator role, CJDS appropriate cjp:config_read or cjp:config_write scopes.

### CJDS Schema

**CJDS Event Data Schema Details**

| Attribute        | Type                         | Description                                                                                                                                                                                                                                                                                                                                                                              | Constraints                                                                                                                                                                     | Examples                                                                                                                                                                                                                                    |
| ---------------- | ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| specversion      | String                       | The version of the CloudEvents specification which the event uses. This enables the interpretation of the context. Compliant event producers MUST use a value of 1.0 when referring to this version of the specification                                                                                                                                                                 | REQUIRED, MUST be a non-empty string                                                                                                                                            | 1.0                                                                                                                                                                                                                                         |
| type             | String                       | This attribute contains a value describing the type of event related to the originating occurrence.                                                                                                                                                                                                                                                                                      | REQUIRED, MUST be a non-empty string, SHOULD be prefixed with a reverse-DNS name. The prefixed domain dictates the organization which defines the semantics of this event type. | com.github.pull_request.opened, com.example.object.deleted.v2                                                                                                                                                                               |
| source           | URI-reference                | Identifies the context in which an event happened. Often this will include information such as the type of the event source, the organization publishing the event or the process that produced the event. The exact syntax and semantics behind the data encoded in the URI is defined by the event producer. Producers MUST ensure that source + id is unique for each distinct event. | REQUIRED, MUST be a non-empty URI-reference, An absolute URI is RECOMMENDED                                                                                                     | https://github.com/cloudevents, mailto:cncf-wg-serverless@lists.cncf.io, urn:uuid:6e8bc430-9c3a-11d9-9669-0800200c9a66, /cloudevents/spec/pull/123, /sensors/tn-1234567/alerts, 1-555-123-4567                                              |
| id               | String                       | Identifies the event. Producers MUST ensure that source + id is unique for each distinct event                                                                                                                                                                                                                                                                                           | REQUIRED, MUST be a non-empty string, MUST be unique within the scope of the producer                                                                                           | 1eb65fdf-9643-417f-9974-ad72cae0e10f                                                                                                                                                                                                        |
| time             | Timestamp                    | Timestamp of when the occurrence happened.                                                                                                                                                                                                                                                                                                                                               | OPTIONAL, If present, MUST be a ISO Timestamp                                                                                                                                   | 2018-04-05T17:31:00Z                                                                                                                                                                                                                        |
| identity         | String                       | This describes the identifier to whom the event is produced.                                                                                                                                                                                                                                                                                                                             | REQUIRED, MUST be non-empty                                                                                                                                                     | ram@cisco.com                                                                                                                                                                                                                               |
| identitytype     | String                       | This specifies the type of identifier. It is an Enum. Currently, we support only email, phone and customerId.                                                                                                                                                                                                                                                                            | REQUIRED, MUST be a non-empty string                                                                                                                                            | email                                                                                                                                                                                                                                       |
| previousidentity | String                       | The identity with whom we want to merge the new person's events                                                                                                                                                                                                                                                                                                                          | OPTIONAL, If present, MUST be non-empty                                                                                                                                         | ram@cisco.com                                                                                                                                                                                                                               |
| datacontenttype  | String                       | Content type of data value.                                                                                                                                                                                                                                                                                                                                                              | REQUIRED, If present, MUST adhere to the format specified in RFC 2046                                                                                                           | application/json                                                                                                                                                                                                                            |
| data             | Based on the datacontenttype | The event payload. This specification does not place any restriction on the type of this information. It is encoded into a media format which is specified by the datacontenttype attribute (e.g. application/json), and adheres to the dataschema format when those respective attributes are present.                                                                                  | REQUIRED                                                                                                                                                                        | `{"taskId": "888b688e-b74e-4fa6-8260-1e8bd0a3523a","origin": "ram@cisco.com","destination": "1234567890","direction": "INBOUND","channelType": "email","outboundType": null,"queueId": "AXZvA7uJ1OI4n5klHgJA","createdTime": 160266966391}` |

**Sample CJDS Event Data**

```JSON
{
  "specversion": "1.0",
  "type": "task:new",
  "source": "wxcc",
  "id": "1eb65fdf-9643-417f-9974-ad72cae0e10f",
  "time": "2022-03-14T01:48:45Z",
  "identity": "ram@cisco.com",
  "identitytype": "email",
  "previousidentity": "ramnat@cisco.com",
  "datacontenttype": "application/json",
  "data": {
    "agentId": "109332be-7fc4-4d4d-9488-ebdb8e13b9bbe",
    "destination": "+12147651210",
    "profileType": "BLENDED",
    "currentState": "idle",
    "idleCodeId": "AXUr0jX9H5TuplmIxiC",
    "createdTime": "1645819554383"
  }
}
```
