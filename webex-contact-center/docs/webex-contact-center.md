---
type: Guide
title: Webex Contact Center | Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/webex-contact-center
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-contact-center)

## What's possible with the Webex Customer Experience open platform and APIs?

The Webex Customer Experience platform provides an end-to-end customer experience solution. The open architecture and APIs give you the flexibility to:

- Customize every step of your customer and agent experience
- Integrate with existing business applications and tools
- Build new features and services that are not available out of the box
- Track and improve KPIs
- And much more!

**Note:** You can test the APIs by using the sample IDE (Integrated Development Environment) found right next to the API definition.

## REST

Many of the Webex Customer Experience APIs are RESTful. Each resource is represented by a base URL such as /agents, and you can view the resources under **API Reference** on the left navigation pane. The available methods are listed under each resource. For instance, navigating to **Agents** displays a method GET /agents/statistics. Clicking the method link takes you to a page that fully details the Agent Statistics API.

Within the details of an API, a **Try Out** capability is available to test calling the endpoint. Here you will provide an access token, and any values (if required) in the form of query parameters, path parameters, or the request body. For endpoints which accept query parameters, path parameters or request bodies, the required parameters (if any) are marked with an asterisk (\*). For responses, the APIs currently support return data in the application/JSON format only. Clicking the copy icon in the request box copies the cURL statement, and any values provided to test the API using **Try Out** are filled into the cURL statement.

## GraphQL

Webex Customer Experience has the capability to create tasks which represent the request or demand for work from the agents. These tasks can be defined with varying levels of complexity, as can be created for any type of media - telephony, chat, email, etc. We offer GraphQL APIs to extract only the data that is relevant to your use case and narrow down the output response.

- For details on using the GraphQL APIs, see [Getting started with the Search API using GraphQL](https://developer.webex.com/docs/getting-started-with-search-api).
- You can find the GraphQL APIs in [Search > Search Tasks](https://developer.webex.com/docs/api/v1/search) and test them out using our **Try Out** feature.

## Webhooks

Webhooks form a great system for working with near-real-time data, and for reacting to Customer Experience events using custom logic. If you want to stay on top of a busy contact center, or have an application which can’t wait for slow batch reports or expensive API polling-and-diffing solutions, then you're in the right place.

Go to the [Using Webhooks](https://developer.webex.com/docs/using-webhooks) guide to learn more.
