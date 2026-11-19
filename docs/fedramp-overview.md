---
type: Guide
title: FedRAMP Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/fedramp-overview
content_type: documentation
product_group:
- webex-suite
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/fedramp-overview)

The Webex FedRAMP environment is separate and distinct from our “commercial” environment and is tailored to the Federal government's collaboration business. Access to the Webex FedRAMP environment is for federal government organizations and partners invited by those entities.

## Webex for Government Developer Portal

The Webex for Government developer portal is available at https://developer-usgov.webex.com. This is an access-controlled portal that will allow customers and partners with a Webex for Government Organizations to create Bots and Integrations, seek developer support, and review API reference guides.

The Webex FedRAMP environment is separate and distinct from our “commercial” environment and is tailored to the federal government’s collaborative business. Access to the Webex FedRAMP environment is for federal government organizations and partners invited by those entities.


The environment is specially isolated and secured in accordance with the mandated standards. Consequently, some of the convenience tools supporting application development are unavailable. Instead, partners are encouraged to develop their applications – respecting the API limitations outlined in this document – in the commercial environment and then follow the approach to register their apps for the FedRAMP Webex system as described later here.


Partners that are already familiar with the Webex APIs and therefore do not need the guides, API explorer, blogs, and other support infrastructure from the commercial developer portal will be able to develop apps in the Webex FedRAMP environment directly with the help of the instructions in this document.


The information and instructions in this document are intentionally succinct.


## FedRAMP API URL and Control Hub URL

The Webex APIs in FedRAMP are accessible under api-usgov.webex.com. For example, the message endpoint’s address would be https://api-usgov.webex.com/v1/messages, which is notably distinct from the commercial environment at webexapis.com. Applications for the FedRAMP environment must call that API address alone. The Control Hub login screen is available at [https://admin-usgov.webex.com](https://admin-usgov.webex.com), also separate and distinct from the commercial environment.

The Webex XML APIs used to control the meeting experience are accessed under the site name like the commercial APIs. For example, if one of FedRAMP customer site's name is ‘ABC,’ its DNS is abc.webex.com, and the XML API can be accessed at https://abc.webex.com/WBXService/XMLService.

## FedRAMP application types

In the Webex commercial environment, a set of application types is available that do not translate directly to the FedRAMP environment. There are Bots (standalone persons), Integrations (acting on a user's behalf), Embedded Apps,  Service Apps, and Guest Issuers (creation of anonymous persons) available in the commercial environment. Guest Issuers are unavailable in FedRAMP, and no substitute is currently planned. Those app types have been intentionally disabled. As such, this document will cover the development of Bots, Integrations and Embedded Apps as its primary goal.
