---
type: Article
title: 'The A-Z of Webex Contact Center APIs: Address Book'
canonical_url: https://developer.webex.com/blog/the-a-z-of-webex-contact-center-apis-address-book
content_type: blog
date: '2024-07-17'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/the-a-z-of-webex-contact-center-apis-address-book)

This is the beginning of a series of blogs called “The A-Z of Webex Contact Center APIs”. In this blog series we will be exploring the entirety of an API and adding context to the effects of executing the API from the perspective of a user. There are two main goals here. First, we want to educate the developer community about what is possible with Webex Contact Center developer tools. Lastly, we want to provoke curiosity amongst Webex developers and expand on the art of possible.

The Webex Contact Center Address Book is a tool available to agents that allows them to select an entry to dial instead of manually entering a phone number when placing a call. Administrators will create an address book and add it to a Desktop Profile that an agent is assigned to. Admins must enable outbound dialing within the dial plan of the desktop profile assigned to an agent that is intended to make outbound calls.

An admin can create an address book from Control Hub. The Control Hub even provides a way for administrators to manage address books in bulk. Below we will go over a way to programmatically manage address books with the Webex Contact Center RESTful APIs.

### Managing Address Books In Control Hub

Before we dive into using the API, it is important to know the expected experience and outcomes of creating an Address Book in the Control Hub. Control Hub is the central interface that administrators utilize to manage a Webex organization, manage users, assign service, view analytics and more.

To create an address book in the Control Hub an administrator would navigate to the *Contact Center > Desktop Experience > Address Book* and click on Create Address Book.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1c2a29e8c89eabb2/wxcc-address-book-api-blog-2.png)

Then the administrator is prompted to fill out a form requiring inputs for the name, a description, Parent Type and Entries for the Address book. The Parent Type defines if the Address Book is available to all sites in an organization, or a specific site in an organization. The Entries are the actual names and phone numbers of contacts in the Address Book.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc0fefe076695ada5/wxcc-address-book-api-blog-3.png)

Once an Address Book is created, it becomes visible in the Address Book section in the Control Hub.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt086548b8f12eafe9/wxcc-address-book-api-blog-4.png)

Then we can drill into the Address Book that we created and manage entries.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte88f2c8033b8e843/wxcc-address-book-api-blog-5.png)

Administrators can also use the Control Hub to add Address Books to an organization in bulk by following the instructions [here](https://help.webex.com/en-us/article/31e39g/Bulk-Operations-in-Webex-Contact-Center).

### Using the Address Book API

Getting started with the APIs for the address book will require an Organization ID. The `orgId` can be obtained from [Control Hub](https://help.webex.com/en-us/article/k5pal8/Look-Up-Your-Organization-ID-in-Control-Hub), or an [access token](https://developer.webex.com/docs/authentication#getting-an-access-token) obtained via the OAuth 2.0 flow for a Webex Contact Center integration application.

#### Address Books

The [Address Book API](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book) supports CRUD (create, read, update and delete) operations so developers and administrators can execute the same functionality we see in the Control Hub, both programmatically and in bulk.

The required parameters in the path and body when executing the [Create an Address Book](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/create-a-new-address-book) API are Orgid, Name, and Parent Type.

Developers can leverage the Address Book IDs provided in the [List Address Books API](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/list-address-books) to do things like, get Address Book details, update an Address Book name, or an update an Address Book description:

- [Create Address Book](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/create-a-new-address-book)
- [Get Address Book by ID](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/get-specific-address-book-by-id)
- [Update Address Book by ID](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/update-specific-address-book-by-id)
- [Delete Address Book by ID](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/delete-specific-address-book-by-id)
- [List Address Books](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/list-address-books)

<br/>

#### Entries

There is also an associated set of APIs, that supports CRUD operations, for an Address Book’s associated entries that an agent can use to make outbound calls. There is also an API for [listing](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/list-address-book-entrys) an Address Book’s entries to get the Entry Id. With Entry Id, a developer can get details about a contact in the Address Book and use them in integrations and automations.

The required parameters in the path and body when using the [Create an Address Book Entry](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/create-a-new-address-book-entry) API are Orgid, Name, and Phone Number.

Developers can leverage the filter, search, and attributes query parameter available in the [List Address Book Entry](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/list-address-book-entrys) API to do things like, get an entry by ID, lookup an entry by a supported attribute (id,name,number), or filter entries by a search keyword:

- [Create Address Book Entry](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/create-a-new-address-book-entry)
- [Get Address Book Entry by ID](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/get-specific-address-book-entry-by-id)
- [Update Address Book Entry by ID](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/update-specific-address-book-entry-by-id)
- [Delete Address Book Entry by ID](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/delete-specific-address-book-entry-by-id)
- [List Address Book Entry](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/list-address-book-entrys)

<br/>

### Bulk Operations

Additionally, there is bulk operation support within the API set available to developers and administrators:

- [Bulk Save Address Book Entry](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/bulk-save-address-book-entrys)
- [Bulk Export Address Books](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/bulk-export-address-books)

<br/>

#### Integrations

When registering an integration where the Address Book APIs are intended to be used, be sure to select `cjp:config_write` or `cjp:config_read` scopes.

#### Potential Use Case

A potential use case for the Address Book API is when a Webex Contact Center organization administrator would like to synchronize an address with data from a CRM or Directory in an automated fashion. [The Bulk Save Address Book Entry API](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book/bulk-save-address-book-entrys) would be the perfect candidate to accomplish this. Look at this [sample code](https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/address-book-sample) to see one way to accomplish this.

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
