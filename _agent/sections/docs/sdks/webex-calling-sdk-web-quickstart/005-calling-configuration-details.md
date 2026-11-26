---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Calling Configuration Details
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Calling SDK. This guide is designed to provide developers with a concise walkthrough to swiftly set up, authorize, and test the core calling functionalities within the Calling SDK.

---

By following the sequential flow of this document and integrating the provided code snippets, you'll be able to authenticate your application and initiate your first calls. Whether you're new to Webex's Calling SDK or looking to brush up on the basics, this guide ensures a streamlined experience to get you up and running in no time. Let's dive in!

## Selected section

## Calling Configuration Details

This is the definition for a `callingConfig` object:

```javascript
callingConfig: {
 clientConfig: {
  calling: boolean,
  contact: boolean,
  callHistory: boolean,
  callSettings: boolean,
  voicemail: boolean,
 },
 callingClientConfig: {
  logger: {
   level: string
  },
  discovery: {
   country: string,
   region: string,
  },
  serviceData: {
   domain: string,
   indicator: string,
   guestName: string
  }
 },
 logger: {
  level: string
 }
}
```

The following tables cover the different configuration attributes present inside the `callingConfig` object.

### Client Configuration



| **S.no** | **Attribute** | **Description** | **Data Type** | **Default Attribute?** | **Public Attribute?** |
| --- | --- | --- | --- | --- | --- |
| 1. | `calling` | Toggles the availability of the `callingClient` module.  | `Boolean` | No | Yes |
| 2. | `contact` | Toggles the availability of the `contactClient` module. | `Boolean` | No | Yes |
| 3. | `callHistory` | Toggles the availability of the `callHistory` module. | `Boolean` | No | Yes |
| 4. | `callSettings` | Toggles the availability of the `callSettings` module. | `Boolean` | No | Yes |
| 5. | `voicemail` | Toggles the availability of the `voicemailClient` module. | `Boolean` | No | Yes |

### Calling Client Configuration



| **S.no** | **Attribute** | **Description** | **Data Type** | **Default Attribute?** | **Public Attribute?** |
| --- | --- | --- | --- | --- | --- |
| 1. | `discovery` |  | `Object` | No | Yes |
| 1.a. | `country` | Country from where the device registration is triggered. It has to be an Alpha-2 code as per ISO 3166-1 standards. Here's the list of [officially assigned Alpha-2 codes from Wikipedia](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements). | `String` | No | Yes |
| 1.b. | `region` | Region from where the device registration is triggered. It should be one of the following: `AP-SOUTHEAST`, `US-EAST`, `EU`, or `EU-CENTRAL`. | `String` | No | Yes |
| 2. | `serviceData` |  it represents the service data of the SDK. | `String` | No | Yes |
| 2.a. | `domain` | Identifies which service is using the Calling SDK. | `String` | Yes | Yes |
| 2.b. | `indicator` | The type of service being used in the SDK. Its value should be `CALLING`, `CONTACT_CENTER`, or `GUEST_CALLING`. | `ServiceIndicator` | No | No |
| 2.c. | `guestName` | The `guestName` attribute is used in the SDK to indicate the name of the guest within a calling service. | `String` | No | Yes |
| 3.  | `logger` | Logger configuration. | `Object` |  |  |

### Logger Configuration



| **S.no** | **Attribute** | **Description** | **Data Type** | **Default Attribute?** | **Public Attribute?** |
| --- | --- | --- | --- | --- | --- |
| 1. | `level` | Maximum log level that should be printed to the console. Possible values:`silent`, `error`, `warn`, `log`, `info`, `debug`, `trace` | `String` |  | Yes |
