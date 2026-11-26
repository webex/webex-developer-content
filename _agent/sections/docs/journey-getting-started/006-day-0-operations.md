---
type: Excerpt
canonical_url: https://developer.webex.com/docs/journey-getting-started
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Day 0 Operations
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/journey-getting-started). [Full Markdown](../../../../docs/journey-getting-started.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Cisco Journey Data Service (CJDS) is a journey management service that helps organizations turn raw customer data into real-time insights and actions. It enables businesses to unify identity, track intent signals, and drive smarter, more personalized interactions through Webex Contact Center.

## Selected section

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
