---
type: Guide
title: Customer Journey Data FAQ | Consolidated Guide
display_title: FAQ
canonical_url: https://developer.webex.com/docs/journey-data-service-faq
content_type: documentation
product_group:
- webex-suite
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/journey-data-service-faq)

Find answers to frequently asked questions about Journey Data Services.

## What is CJDS, Customer Journey Data Service?

Customer Journey Data service (CJDS) is a next-generation customer journey management service empowering organizations to go from Data to Insights to Action. CJDS enables businesses to capture customer journeys across any channels/application, identify insights and take real-time actions to provide an excellent customer experience.

## For what target audience is CJDS most relevant?

Multiple stakeholders can leverage this platform, including customer experience/service, sales, operations, marketing
strategists, and customer communication professionals, to visualize/map the entire customer journey and take real-time
actions to make it more personalized, timely, and impactful. CJDS is currently API first, but the Cisco team is working to
provide a low code/no-code visual experience in future releases.

## What is CDP? How is CJDS like/or interact with a CDP?

A customer data platform (CDP) is software that collects and unifies first-party customer data—from multiple sources—
to build a single, coherent, complete view of each customer. CJDS can integrate with any data source, including a CDP,
and act as a layer to identify, analyze, and orchestrate customer journeys.
What differentiates CJDS from a CDP further is the ability to orchestrate and trigger actions in real-time – this is where
our CJDS service stands out!

## What data security measures does CJDS have?

CJDS is a product built within Cisco and will meet all industry practices and regulatory requirements in its release
version. In addition, we are currently targeting SOC2 certification and other specific compliance certifications based on
geographical requirements.

## How is CJDS different from campaign management or marketing automation tools? What is Cisco’s key differentiator?

CJDS can integrate multiple data sources, including marketing and campaign management tools, and act as an
analytical/orchestration layer for the entire customer lifecycle. Our early adopters have used CJDS to empower their
existing marketing and campaign management tools to orchestrate real-time actions.

## Do I need to migrate to leverage CJDS services and implementation?

CJDS fully integrates with the existing contact center, CRM solutions, and other platforms – both on-premises and in the
cloud. In addition, CJDS offers multiple ways of collecting data from various touchpoints by leveraging API-level
integration with other third-party services or preconfigured Cisco integrations (like with Webex Connect for digital channels, Webex
Contact Center, etc.)

## How long does CJDS take to implement?

The integration depends on several factors. For example, how many datapoints and touchpoints need to be integrated?
What backend systems are in place? What contact center is currently in use and is it on-premises or in the cloud?
The integration is currently completely API-driven and with that, CJDS can integrate with nearly and existing contact
center, including collecting data and information from any channel and back-end applications.
Some of these use cases may take days to integrate, other with more customizations require more effort – however,
Cisco’s CJDS service is meant to simply integrate within any customer engagement workflow and easy to “connect”,
“modify” and “customize” is one of the major key advantages of our service.
Cisco recommends customers start with a journey that touches 2-3 channels with business rule logic of low to medium
levels of complexity, which can be up and running with just a few weeks' work. However, the duration of the initial
journey is often dependent on access to the customer's data, channel touchpoints, and subject matter experts.

## What CRM vendors does CJDS work with?

As of now, Cisco CJDS can integrate with any CRM platform by leveraging our existing and available APIs. However, in
the next upcoming milestones of our roadmap, we will provide out-of-the-box integrations with major CRM platforms
and services.

## What does CJDS cost, how can I purchase CJDS?

CJDS will be available with Contact Center Flex 3.0 offering. For more details, please review the offer details here - https://www.cisco.com/c/en/us/products/collateral/customer-collaboration/collab-flex-3-contact-center-ds.html

## Is there anything CJDS cannot integrate with?

We can integrate with any service (on-premises or cloud) that provides API capabilities or
other mechanisms to collect data and information.

## How will partner integrate CJDS and widgets into customer care environments for “their” customers?

We have the customer journey widget (omnichannel) publicly available on our GitHub repository. Any
customer or partner can integrate their respective data sources (voice, digital channels, 3rd party tools) and plug this
widget into their existing contact center solution to enable their workforce to see the entire customer
journey and use these data points to provide a personalized, timely, and impactful experience to their customers

## How does CJDS create customer profiles? And how are they different from the CRM customer profiles?

Customer Journeys are only as good as the context they capture, and with every journey there is a human customer
profile that needs to be known, otherwise the context would be lost. Context can be built incrementally as the journey
progresses, instead of at all once. While CRM may hold the bio essentials - it remains a static snapshot. Progressive
profiles are much more than a static record profile that may be held in the CRM.
These profiles are dynamic and living as they capture interests - intent and details over time. Context is a significant
advantage to both agent and AI models in today’s setting. Consider for instance, an existing checking account customer
who browses auto loans online before calling in for a routine service request for banking, this may provide an
opportunity for a cross-sell while behind the scenes “ensemble routing” can override the IVR and route directly to
connect with an agent who has auto loan quoting competency, in-addition to general servicing to make serendipity
more likely.
