---
type: Guide
title: Getting Started with CJDS
display_title: Getting Started with CJDS
canonical_url: https://developer.webex.com/docs/journey-getting-started
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/journey-getting-started)

Cisco Journey Data Service (CJDS) is a journey management service that helps organizations turn raw customer data into real-time insights and actions. It enables businesses to unify identity, track intent signals, and drive smarter, more personalized interactions through Webex Contact Center.

## CJDS Overview

Cisco Journey Data Service is an API-driven service designed to empower organizations to harness customer data and transform it into actionable insights. By leveraging CJDS, companies can seamlessly integrate, analyze, and act on diverse data sources to optimize customer interactions. The service is built on four core capabilities:

1. **Listen:** Ingest data from any source, whether internal systems or third-party applications, to gather insights from disparate data streams. This capability allows CJDS to continuously monitor customer interactions and behaviors across all channels.
2. **Identify:** Build dynamic customer profiles by capturing critical propensity drivers, such as preferred communication channels, languages, and behavioral patterns. This step ensures a unified view of each customer, enabling better personalization.
3. **Analyze:** Utilize powerful aggregation techniques to process collected data, transforming it into meaningful insights. These insights can uncover patterns, trends, and opportunities for enhancing customer engagement.
4. **Act:** Leverage CJDS insights to optimize customer journeys in real-time. By integrating with the Webex Contact Center's flow control and orchestration capabilities, CJDS can intelligently route interactions based on customer profiles. Additionally, these insights are surfaced to agents through the Agent Desktop, providing real-time contextual data to enhance customer support.

## Key Capabilities Breakdown

The four foundational pillars of CJDS translate into specific API functionalities:

1.	**Data Ingestion:** Use **Listening APIs** to capture data from various sources, enabling continuous monitoring and enrichment of customer profiles.
2.	**Customer Identification:** Leverage the **Create a Person API** and **Merge API** to build and maintain dynamic customer profiles, consolidating data across different channels and interactions.
3.	**Profile Creation & Insights:** Utilize the **Profile Template APIs** to transform raw data into actionable insights, ensuring a robust understanding of customer behaviors and preferences.
4.	**Trigger Actions:** Implement the **Action APIs** to trigger automated workflows using business rules, enhancing customer experience and optimizing contact center operations.

## Key Onboarding Collateral

- [CJDS Overview Vidcast](https://app.vidcast.io/share/889c2cbf-51b2-4cc9-94f8-9143078dca83)
- [Customer Journey Widget Overview](https://app.vidcast.io/share/50d7fbc9-4fb3-4014-9337-98ccb2d874c3)
- [Journey - Getting Started](https://developer.webex.com/docs/journey-getting-started)
- [Journey - API documentation](https://developer.webex.com/docs/api/v1/profile-creation-and-insights)
- [API Deep Dive Webinar](https://app.vidcast.io/share/434bfd8f-f783-4800-9e27-73026edb7553)
- [How to integrate journey widget with your agent desktop?](https://help.webex.com/tfcmrp)
- [Use Case Vidcast (Personalized Customer Experience)](https://app.vidcast.io/share/0052e897-6d7a-4de5-8795-8926f0516503)
- [Use Case Vidcast (Digital Channels & Webpage Use Case)](https://app.vidcast.io/share/b90e50f4-d085-416c-9aae-29426fa18f53)

## Provisioning CJDS for Your Organization

Follow these steps based on when your Webex Contact Center Org was created:

- If your org was created before October 31 , 2025
  → No action needed. CJDS is automatically linked to your Org ID.

- If you’re already using CJDS with a custom layout
  → No changes required. Your existing setup is supported.

- If your org was created after November 1, 2025
  → Complete this [form](https://ciscocx.qualtrics.com/jfe/form/SV_0oFIX1j9BUbh3f0) to request CJDS provisioning. A journey tenant will be created within 72 hours.

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

## Day 0 Operations

To use CJDS with Webex Contact Center:

- The designated **Customer-Journey-Widget** journey project is configured automatically.
- Add user identities to a journey project.
- Enable the Customer Journey Widget on an agent desktop.

### Webex Contact Center event routing

Webex Contact Center events automatically flow to the designated **Customer-Journey-Widget** workspace. You don't need to activate or configure a Webex Contact Center connector anymore.

For existing organizations, Contact Center events continue to flow to the workspace already associated with Webex Contact Center. For newly onboarded organizations, the designated default workspace is configured automatically.

Only one workspace receives the default Webex Contact Center event feed. You can continue to create and use additional journey projects for custom data sources, such as CRM events. However, you can't change, disable, or reassign the workspace used for the default Contact Center event feed.

To verify the integration, confirm that Contact Center events appear in the **Customer-Journey-Widget** workspace and in the Customer Journey Widget in Agent Desktop.

### Create an additional Journey Project

Create an additional journey project only if you want to ingest or manage custom data sources, such as CRM events. The designated **Customer-Journey-Widget** journey project is used for default Webex Contact Center events.

Journey projects help organizations manage multiple data sources. Each journey project has a unique identifier which is required to leverage CJDS API payloads. Note that project IDs in Control Hub are referred to as workspace IDs in APIs.

1. Sign in to Control Hub and go to **Customer Journey Data** \> **Journey projects**.
2. Click **Create a journey project**.
3. Enter a name and a description for the journey project.

### Add Customer Identities to a Journey Project:

There are two ways to add your identity today.

#### 1. CSV Upload

Adding customer identities to JDS will help you connect multiple customer identifiers (phone number, email address, Customer ID) to a single customer identity. You can upload a CSV file with multiple user identities. The requirements for the CSV file are the following:
- Required headers:
  - Id
  - First Name
  - Last Name
  - Email Addresses
  - Phone Numbers
  - Customers Ids
- Each customer identity can have up to five email addresses, phone numbers, and customer IDs, separated by a | (pipe) symbol.
- Each customer identity must have at least an email address, phone number, or customer ID or else the CSV file will return an error.
- For the Id column, make sure to leave each row empty. When you upload the CSV file, this field will auto-generate.

![](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta88737619feb7451/69b1e8657e503c0053b2de79/customer_identity_9d4fbd6158.png)

Once you create a CSV file, you can upload that file to a journey project that you created.

1. Sign in to Control Hub and go to **Customer Journey Data** \> **Journey projects**.
2. Select a journey project that you want to create user identities for.
3. Select **Identities**.
4. Click **Create an identity**.
5. Upload a CSV file that you created for customer identities, and then click **Next**.
6. If the CSV file is valid, a window appears to show you if the import was successful. Once you're done, select **Close**. You should see a list of all the uploaded customer identities.

![](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta24bd93cc11034d0/69b1e866204a7061f8030fbe/journey_projects_identities_view_6befa28ca3.png)

#### 2. Real-Time Identity Creation via Flow

Use the Create Person API in Flow Designer to sync real-time identity data

Example:

- A caller enters the IVR

- You fetch customer details from CRM

- Use HTTP Node (for contact center flow) or dedicated Journey Node (Connect flow) to call CJDS API and create/update identity profile on the fly

This keeps CJDS aligned with your system of record.


### Enable the Customer Journey Widget

The Journey Widget provides agents with a unified view of a customer’s real-time and historical interactions across all integrated systems.

To activate - Follow [this guide](https://help.webex.com/en-us/article/tfcmrp/Customer-Journey-Widget-Version-10-for-Webex-Contact-Center) to embed it into the Webex Agent Desktop layout.
