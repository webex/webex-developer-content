---
type: Guide
title: Webex Assistant Skills Developer Portal Guide | Consolidated Guide
display_title: Skills Developer Portal
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-guide-developer-portal-guide
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-assistant-skills-guide-developer-portal-guide)

The Assistant Skills Developer Portal is a tool for skills developers to create and manage their skills' association to the Assistant skills service.

---



> **Warning**
>
> No new features are being added to Webex Assistant Skills and only skills added through May 2025 are directly supported by Cisco.



## What is the Assistant Skills Developer Portal

The **Assistant Skills Developer Portal** is a tool for skills developers to create and manage their skill's association to the **Assistant skills** service. The Developer Portal is located at [https://skills-developer.intelligence.webex.com](https://skills-developer.intelligence.webex.com).




> **Info**
>
> This site is not where organization administrators manage skills enablement for their organization. Managing organization-level access to skills can be done in [Control Hub](https://admin.webex.com) by a full-administrator. Once a skill is created in this portal, the content will be viewable in Control Hub. By default, all skills are disabled.



We'll go through the following topics in this guide, which will explain how to use this tool:

- [Overview](https://developer.webex.com/docs/webex-assistant-skills-guide-developer-portal-guide#overview)
- [Log in](https://developer.webex.com/docs/webex-assistant-skills-guide-developer-portal-guide#log-in)
- [Creating a Skill](https://developer.webex.com/docs/webex-assistant-skills-guide-developer-portal-guide#creating-a-skill)
- [Managing your Skill](https://developer.webex.com/docs/webex-assistant-skills-guide-developer-portal-guide#looking-at-your-skills)
- [Editing a Skill](https://developer.webex.com/docs/webex-assistant-skills-guide-developer-portal-guide#editing-a-skill)
- [Deleting a Skill](https://developer.webex.com/docs/webex-assistant-skills-guide-developer-portal-guide#deleting-a-skill)
- [Testing a Skill](https://developer.webex.com/docs/webex-assistant-skills-guide#skill-testing)

## Overview

When you first go into the [Developer Portal](https://skills-developer.intelligence.webex.com), you'll land at the **Overview** page. This page offers a high level overview of what skills are and what they can do. Reference the guides on [developer.webex.com](https://developer.webex.com) for the most up-to-date content.

![Overview Page](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta2fb235712c416f9/6171b16c90079752a47e8b4e/overview_page.png)

## Log In

Once you enter the portal, the first step is to log in. For that, you can use the **Log In** button in the top-right corner:

![Log in](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7fb6e0d32d26d906/6171b16cf13b7e5c89d3f3c5/login.png)

In the next few sections, we'll be working on the **Developer** tab. Once logged in, go into the **Developer** section.

## Creating a Skill

To create a skill, click **Create New Skill**:

![Create Skill Button](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3ccad7234e5d1939/6171b16c5422ab67be73daa5/create_skill_button.png)

You will now be presented with a form that you need to complete in order to create the skill:

![Create Skill Form](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt997216ec8bbba0a0/6171b16cfd37c069473b032a/create_skill_form.png)

The details you need to fill in are the following:

- **Name**: The name of your skill.
- **Description**: An optional description of what this skill does.
- **Home Page**: An optional URL to a website with more information about the skill.
- **Invocation Names**: Keywords that end-users will use to invoke the skill on a Webex Device.
- **Languages**: The list of languages that your skill can support.
- **URL**: URL endpoint to your skill code.
- **Contact Email**: Email of who should be contacted with inquires about the skill. 
- **Secret**: Private string used by the Assistant Service to identify itself to the skill. This string is configured in the application code.
- **Public Key**: A RSA public key needed to securely communicate between the **Assistant skills** Service and the skill.
  
Fill in **all** the fields with your skill details above. When ready, click **OK**.

![Create Skill](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd14f2e024c432144/6171b16c385f7a513f0de935/create_skill.png)

## Managing your Skill

Once you have created at least one skill, it'll display in the **Developer** section as follows:

![Skills List](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1e15f5bfeff48efc/6171b18052c42c67c026d515/skills_list.png)

There are six columns of data associated with your skill. We have already mentioned a few of them in the [Creating a Skill](https://developer.webex.com/docs/webex-assistant-skills-guide-developer-portal-guide#creating-a-skill) section. The ones we didn't cover are:

- **Public**: An indicator showing if the skill has been made public to all Webex sites. Note: Only skills built by Cisco can be made public at this time.  
- **Last Active Time**: Last time the skill was connected (if available).
- **Actions**: This column contains two buttons **Edit** and **Delete**, which we explore in upcoming sections.

Form errors are highlighted in red, for example:

![Skill Create Error](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta88b4e22e5b8f1c6/6171b1765422ab67be73daa9/skill_create_error.png)


## Editing a Skill

Want to edit one of the form fields for the skill? Click the **Edit** button for the skill:

![Skill Edit Button](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5f3352ad70de02ba/6171b17652c42c67c026d511/skill_edit_button.png)

This will open a drawer from the right where we can see a **Skill** tab.

![Skill Tab](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltacb5a2d762c22eea/6171b180f13b7e5c89d3f3cd/skill_tab.png)

If you want to make modifications, click the blue **Edit** button:

![Skill Blue Edit Button](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8a3bdb7f86e8e0d7/6171b1768dfe0f5a8de0a3f7/skill_blue_edit_button.png)

The form to edit your skill displays. As an example, we have added a new invocation name to our sample skill:

![Skill Edit Form](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta0eb14c7143601e0/6171b1804307ab590944c526/skill_edit_form.png)

Save the changes by clicking **OK** at the bottom of the form:

![Skill Edit OK Button](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbde4cb97c8754f33/6171b1805422ab67be73daad/skill_edit_ok_button.png)

We should now see the updated skill:

![Skill Updated](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2bdf7969f7bf8328/6171b180b4d91b5dd10942de/skill_updated.png)

## Deleting a Skill

To delete a skill, click the **Delete** icon:

![Skill Delete Button](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2e19b63dd95a1f5d/6171b176f13b7e5c89d3f3c9/skill_delete_button.png)

You should see a confirmation dialogue. Click **Delete** in order to delete the skill:

![Skill Delete Confirmation](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt532a70e0a494a00f/6171b176b05858694858c50f/skill_delete_confirmation.png)

You should see the skill has been deleted:

![Skill Deleted](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt81c64d905e1a4dd3/6171b176385f7a513f0de939/skill_deleted.png)
