---
type: Guide
title: Guest-to-Guest Sandbox
display_title: Guest-to-Guest Sandbox
canonical_url: https://developer.webex.com/docs/g2g-sandbox
content_type: documentation
product_group:
- webex-suite
categories:
- create
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/g2g-sandbox)

Access your very own Webex Sandbox for building and testing new guest to guest applications.



To request or manage this sandbox, open the [official portal page](<https://developer.webex.com/docs/g2g-sandbox>) and sign in.

[Need a Suite Sandbox?](<https://developer.webex.com/docs/developer-sandbox-guide>)

---



> **Info**
>
> If you're creating a sandbox in the Webex for Government (FedRAMP) portal, please be aware that the sandbox supports commercial APIs rather than FedRAMP-only APIs.



## Introduction

A Developer Sandbox provides you with administrator access to a licensed Webex organization you manage using [Webex Control Hub](https://admin.webex.com) . A licensed org lets you create and test capabilities of the Webex platform not available with [Webex free plans](https://help.webex.com/en-us/article/vyuo1j/Webex-free-plans-%7C-Supported-countries-and-regions#id_133759) (see [Do I need a Developer Sandbox?](https://developer.webex.com/docs/developer-sandbox-guide#do-i-need-a-developer-sandbox) for details).

## Sandbox Quick Start

If you are [signed in](https://developer.webex.com/login) to the Developer Portal when you request a sandbox, the credentials for your new account are sent to the email associated with your Webex account; if you are not signed in you will be prompted to provide an email.

**To request a Sandbox Organization**:

 1. Click **Request a Sandbox** at the top of this page.

    If you want your sandbox to be configured with the all the features of the new **Webex Suite Meeting 
    Platform**, please contact [support](https://developer.webex.com/support) requesting that configuration. This is particularly important if you want to test 
    and execute the [space meeting migration flows](https://developer.webex.com/docs/space-meetings-migration). 
    The standard sandboxes are configured with the legacy meetings platform. Please also refer to [this document](https://developer.webex.com/docs/app-programming-interface-behavior-changes) for differences.

 3. Click **Accept** in the dialog box that appears. Enter your email address, if prompted, then click **Submit**.

    

> **Info**
>
> If the Submit button doesn't work try signing out of your Webex account and then trying again, providing your email address when prompted.



 4. Check your email for the account credentials for your admin account. The email will be titled "Collab Toolbox Provisioning Notification".

## Sign in to Your Account

The provisioning email you receive contains the following information for your sandbox organization:

* Organization name: (e.g. jdoessandboxtest-1xep)
* Username/email: (e.g. admin@jdoessandboxtest-1xep.wbx.ai)
* Password
* Webex Site URL: (e.g. jdoesandboxtest-1xep.webex.com)

To avoid any potential conflicts with your primary Webex account it's recommended that you use a private or incognito browser window to perform the sign in.

**To sign in to Control Hub for your org**:

1. Open a new browser window, or open a private/incognito window (Ctrl+Shift+N or Cmd+Shift+N on Chrome for Windows or MacOS, or Ctrl+Shift+P or Cmd+Shift+P on Firefox for Windows or MacOS).

    

> **Info**
>
> We recommend using the latest desktop version of Google Chrome or Mozilla Firefox. Other browsers may produce unexpected results. Webex Control Hub is not designed for mobile devices.



2. In the new/private browser window open [Webex Control Hub](https://admin.webex.com). You may need to copy and paste the URL (`https://admin.webex.com`) into your browser if the link doesn't open in the new/private window.
3. In the sign in form enter the username/email address from the provisioning email.
4. Enter the password from the provisioning email.
5. Click **Accept** to agree to the terms of service.

And that's it! You now have your very own Sandbox for testing your Webex apps. See [Next Steps and Learn More](https://developer.webex.com/docs/developer-sandbox-guide#next-steps-and-learn-more) to learn what you can do.


## Next Steps and Learn More

This section contains details about how to use your Developer Sandbox.

**Using Webex Control Hub** &mdash; [Webex Control Hub](https://admin.webex.com) is how you manage and monitor all aspects of your Webex organization. See [Get Started with Webex Control Hub ](https://help.webex.com/en-US/article/nkhozs6/Get-Started-with-Control-Hub) for an introduction to what you can do with Control Hub.

**Adding Users to your Organization** &mdash; You'll likely want to invite users to join your sandbox organization. The easiest way is to [manualy add users](https://help.webex.com/en-us/article/v71ztb/Add-Users-Manually-in-Control-Hub). You can also [assign roles to your users](https://help.webex.com/en-us/article/fs78p5/Assign-organization-account-roles-in-Control-Hub).



> **Warning**
>
> Users invited to join your sandbox organization must **not** use an email associated with an existing Webex account. Admins should use alternate email addresses to invite users with existing Webex accounts.



**Making Admin API calls** &mdash; To use the [Admin](https://developer.webex.com/docs/admin) or [Compliance](https://developer.webex.com/docs/compliance) APIs you'll need to generate authentication tokens using your sandbox administrator account, or other admin user you've added to your organization. Similarly, to use the **Try It** feature in the [interactive API reference](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting) as an admin, you will need to [sign in to the Developer Portal](https://developer.webex.com/login) with your sandbox's administrator account credentials.

**Create and Manage Embedded Apps** &mdash; Any user in your sandbox organization can [create an embedded app](https://developer.webex.com/my-apps/new/embedded-app) via the Developer Portal. Users must [sign in](https://developer.webex.com/login) using their sandbox org credentials, not with their main Webex account.

To make embedded apps available to other users in your sandbox organization, the app must be [submitted for approval](https://developer.webex.com/docs/embedded-apps-guide#request_approval) by the user who created the app, and [approved](https://help.webex.com/en-us/article/y1eqyd/Embedded-apps-in-Webex#Cisco_Task_in_List_GUI.dita_embeddedapp1) by an organization admin. See the following links for more information.

* [Creating an Embedded App in the Developer Portal](https://developer.webex.com/docs/embedded-apps-guide#creating-an-embedded-app-in-the-developer-portal)
* [Submitting an Embedded App for Approval](https://developer.webex.com/docs/embedded-apps-guide#request_approval)
* See [Managing Embedded Apps](https://help.webex.com/en-us/article/y1eqyd/Embedded-apps-in-Webex) to learn how to approve embedded apps.

Other resources:

- [Get Started with the Webex App](https://help.webex.com/en-US/article/n3xx7vcb/Get-Started-with-Webex-App)
- [Webex Help Resources](https://help.webex.com/en-us)

## Do I need a Developer Sandbox?

A Developer Sandbox provides you with admin access to a licensed Webex organization. A licensed org is required if you need to test features of the Webex platform not available to [Webex free plans](https://help.webex.com/en-us/article/vyuo1j/Webex-free-plans-%7C-Supported-countries-and-regions#id_133759). Specifically, access to a licensed organization is required to perform the following development and testing tasks:

* Create and test [Webex Embedded Apps](https://developer.webex.com/docs/embedded-apps).
* Create integrations that require [admin](https://developer.webex.com/docs/admin) and [compliance](https://developer.webex.com/docs/compliance) API testing.
* Test Webex Messaging bots and integrations in locked (moderated) spaces.

If you aren't developing these types of apps or features you don't necessarily need a Developer Sandbox to develop and test your code.



> **Info**
>
> Each Webex Developer Sandbox use is limited to a maximum of 10 account users for validation and test purposes only. Cisco may from time to time audit Webex Developer Sandbox accounts and reserves the right to remove users in excess of 10 account users, or terminate the Webex Developer Sandbox environment for any Developer resource misuse.



## Ask the Experts

- If you're having trouble accessing your new Sandbox, please reach out to Devsupport@webex.com or go to [Developer Support](https://developer.webex.com/support)


## Terms and Conditions

Please see [Terms of Service](https://developer.webex.com/terms-of-service) for the Webex developer terms and conditions.
