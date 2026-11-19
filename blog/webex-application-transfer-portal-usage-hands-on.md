---
type: Article
title: Webex Application Transfer Portal Usage Hands-on
canonical_url: https://developer.webex.com/blog/webex-application-transfer-portal-usage-hands-on
content_type: blog
date: '2024-11-08'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-application-transfer-portal-usage-hands-on)

You can transfer Webex applications like Integration, Service App, Embedded App, or Bots between users via the Application transfer portal at https://applications.webexbots.cloud/, managed by the Webex Developer Support team. Only a full administrator of a Webex org can manage this tool, and transfers must stay within the same org.

This blog post provides a comprehensive guide for administrators on how to transfer an application from one user to another and addresses some common questions about this tool.

### Walkthrough of the Application Transfer Portal

The application transfer portal mentioned above can be reached at [https://applications.webexbots.cloud/](https://applications.webexbots.cloud/), and it is utilized to manage various types of apps available in Webex, such as Webex Integrations, Service Apps, Embedded Apps, and Webex Bots.

A full administrator must sign in via the Webex page using the provided URL to access the app transfer portal. After authorization, a welcome message appears in the top-left panel, and the user is directed to the **Org Application** page listing available applications in their Webex org.

The left-hand side panel of the portal lists three options as described below.

#### Org Application page

This is also the portal's home page, listing all the applications of the organization. It shows active users, inactive users, and apps from past employees. Even orphaned apps can be transferred to an active user within the Webex organization.

#### My Application Page

This lists all active applications owned by the current authorized administrator user in the portal.

#### Search Page

The Search page lets you refine a Webex application using various options:

- **Created By (personEmail):** This filter is applicable to all types of applications, including Webex Integration, Service App, Embedded App, and Webex Bot. To display an application, it is necessary to input the email address of its creator.
- **Created By (personId):** Similar to **Created By (personEmail)**, but it requires the creator's person ID. This ID can be obtained using the Webex REST API's [/list-people](https://developer.webex.com/docs/api/v1/people/list-people) endpoint.
- **ApplicationId:** Use this identifier to locate a particular application by its unique ID, which can be accessed on the app details page in the Webex Developer portal.
- **Integration (clientId):** This filter is specifically for Webex Integration. To use it, you need to supply the Integration Client ID from the Integration details page on the Webex Developer portal.
- **Bot (personId) and Bot Email:** These filters apply solely to Bots. The Bot email corresponds to the Bot's username, and you can retrieve the Bot's person ID using the [/list-people](https://developer.webex.com/docs/api/v1/people/list-people) API.

These filters help you efficiently find and manage Webex applications.

### How to Transfer an Application Through the Portal

The Search page lets you locate and transfer specific Webex applications within the same Webex organization. You can also move apps from the **Org Applications** or **My Applications** pages by selecting their corresponding checkboxes.

For large orgs with many active applications, the **Seach** page really simplifies finding the required app for transferring.

To transfer the applications:

1. Once the required apps are listed to be transferred on the **Search** page or in the other app details pages, select one or multiple apps using the corresponding checkbox.
1. Click the highlighted **Transfer App** button on the top panel of the portal.
1. Enter the **New Owner** email in the text box and select **Execute Transfer**. Please ensure the new owner's email belongs to the same org.
1. After a successful transfer, an acknowledgment appears. From there, the administrator should ask the new app owner to check the [/my-apps](https://developer.webex.com/my-apps) page to confirm the transfer.

By following these four straightforward steps, a full administrator can efficiently transfer any Webex application to a new user within their organization using this portal.

### FAQs

**Q.** Can only a full administrator of a Webex org transfer an application successfully, or can other admin types like Device Admin, Site Admin, or Partner full administrator do it too?

**A**. No, only a full administrator of an org can access this portal and transfer the applications.

**Q**. Is it possible to transfer multiple apps at once through this portal?

**A.** Yes, this tool allows the transfer of multiple Webex apps. Simply check the boxes for the apps you want to transfer.

**Q**. Is it possible to transfer multiple apps to multiple users at once through this portal?

**A**. No, many-to-many operation currently not implemented in this portal but is planned for a future enhancement.

**Q**. How long should it take to get an app transferred to the new owner once the task is completed?

**A**. It should be an almost real-time update. The new application owner can check under their account on the Webex Developer portal's [/my-apps](https://developer.webex.com/my-apps) page.

**Q**. Is it possible to transfer an application to someone outside of the user's org?

**A**. No. A full administrator of the org can only transfer the apps to an internal user.

**Q**. Can an application be transferred if its owner has left the company?

**A**. Yes, such an application is referred to as an orphan application. If it remains active within the Webex organization, it can be successfully identified and transferred to another member of that organization.

### Engage with us

In case you have any further queries on this or if you are still facing some difficulties while trying to transfer an application to someone, please reach out to our Developer Support team following the instructions provided on our [Webex Developer Support](https://developer.webex.com/support) page.

You can also join our [Webex Developer Community](https://community.cisco.com/t5/webex-for-developers/welcome-to-the-webex-for-developers-forum/m-p/4558386#M321) forum which has dedicated topics, discussion groups, and announcements. We encourage you to tell us about your experience using the Application transfer portal in our community forum.
