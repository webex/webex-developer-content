---
type: Guide
title: Partner Usage of API
display_title: Partners API Guide
canonical_url: https://developer.webex.com/docs/partner-usage
content_type: documentation
product_group:
- webex-suite
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/partner-usage)

This page serves as partner specific "hints" guide for the general Webex APIs

## Who is this guide for?

Our partner community who utilizes Webex APIs will find this guide extremely helpful. If you're a reseller partner who manages customers and users, or an ISV partner that incorporates our app frameworks into your services, there's something for you here. For comprehensive information about Webex API functionality, head over to the [Webex developer portal.](developer.webex.com.)

## What is a Managed Customer?

As a reseller partner, you're typically reselling Webex services to your customers, managing their set-up and users. You might be catering to large corporations or the SMB market; regardless, you share a common need for a streamlined, automated provisioning process. Through this process, your system interacts with Webex APIs to carry out tasks relating to user configuration, licensing, and provisioning within customer organizations. These customers maintained by you are referred to as managed customers.

## How to Utilize API Functions and Admin Roles

Webex APIs offer a robust set of functions for Webex Meeting, Webex Calling, Webex Devices, Webex Chat, and more. You can explore these in detail at developer.webex.com.

Two crucial roles to understand are the organization admin and the partner admin. An organization admin carries out API functions within their own organization, while a partner admin (or delegate) can perform functions in a customer's organization despite being from a different home organization. A partner delegate can be successful in invoking the Webex APIs with a sound understanding of the underlying principles. For more on admin roles, check out this [help article.](https://help.webex.com/en-us/article/16gmxfb/Assign-administrator-roles-in-Partner-Hub)

## Navigating the Managed Partner List

Each partner admin has a list of managed organizations linked to their account. When you invoke an API on a managed customer organization, the system checks if you have the necessary rights to act on that organization. If your managed customer list is not up to date you likely will receive a 403 http status code and you will need to update your managed partner list.

## How to Update Your Managed Partner List

As a partner admin, you have multiple ways to update your managed organizations list. You can directly log in to the customer's Control Hub (admin.webex.com), or you can rely on certain API endpoints that dynamically update your list. For more control, you can use the GET /organizations/{id} command. If the {id} belongs to a managed organization, your partner admin account will be updated but only for the next 24 hours.

## Limitations and Best Practices

Remember, you can't manage more than 2000 organizations in your list. If you add another one, a previous entry will be removed. Also, any organization added through Dynamic Patch will be removed from your list after 24 hours. To effectively manage your list, use the GET /organizations/{id} command before making API calls. If you're dealing with more than 2000 customers per day, you may need to repeat this process.
