---
type: Guide
title: App Hub Submission Checklist for Embedded Apps
display_title: Submission Checklist for Embedded Apps
canonical_url: https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps
content_type: documentation
product_group:
- webex-suite
categories:
- app-hub
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps)

Use these checklists to make sure your Embedded App is ready for submission to App Hub.

## Embedded App Review Process Overview

The Embedded App review process usually takes one to three weeks based on the completeness of your submission. Once you submit your app, your initial point of contact and someone from the Webex App Hub team will work with you throughout the review process.



> **Info**
>
> Cisco performs testing on all Embedded Apps before listing on the Webex App Hub.



After approval, if your app is not functional or the information provided is invalid, the app will be removed from App Hub immediately. Rest assured we will notify you, provide support, and allow you to fix the issue so you can relist your app on the App Hub as soon as possible.

## Business Checklist

* [Branding](https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps#branding)
* [Quality Management](https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps#quality-management)
* [Privacy Policy](https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps#privacy-policy)
* [Contact Information](https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps#contact-information)
* [App Name and Logo](https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps#app-name-and-logo)

<a id="branding"></a>

### Branding

Learn more about Webex by Cisco’s branding considerations:

* [Launch Partner Brand Guidelines and Logos](https://resources.webex.com/webex/integration-partners?guest_pw=ee9ec6b533f59d511dbf94f7599c8c043294ae11111c71c5e3945aec2032c43b)
* [New Webex Suite and Branding](https://help.webex.com/en-us/jil5i/New-Webex-Suite-and-Branding)

Ensure that: 

<ul>
    <li><input type="checkbox"> Your app contains no references to Cisco in any links, including email addresses and descriptions.</li>
</ul>

<a id="quality-management"></a>

### Quality Management

Help us help your app thrive in the Webex ecosystem by creating a compelling internal landing tile surface and external Landing page to persuade users to enable your Embedded App and to help them get started.

Ensure that:

<ul>
    <li><input type="checkbox"> Your app serves a valid Webex end user need.</li>
    <li><input type="checkbox"> Your app is in production and fully operational (no “proof of concepts” or demo apps).</li>
    <li><input type="checkbox"> Your app’s description doesn’t include any mention of “demo”, “alpha”, or similar term.</li>
    <li><input type="checkbox"> Your app’s description is in English (the developer site can be in another language) and free from grammatical errors, and includes the following:</li>
        <ul>
            <li><input type="checkbox"> <strong>App benefits</strong>: An explanation of your app’s use cases and user benefits.</li>
            <li><input type="checkbox"> <strong>How to get started</strong>: A summary on how the user can get started your app.</li>
            <li><input type="checkbox"> <strong>Third-party accounts</strong>: Indicates if the app requires the user to create an account other than a Webex account.</li>
            <li><input type="checkbox"> <strong>Pricing</strong>:Indicates the app’s business model. If the app is free to use, indicate so. Otherwise, include an additional sentence that states the app’s business model (for example, free or paid accounts), and includes a link to where users can find more information on pricing.</li>
        </ul>
    <li><input type="checkbox"> The producer of the app is a real company.</li>
    <li><input type="checkbox"> The app owner details are valid.</li>
    <li><input type="checkbox"> The app is meant for specified workstreams (for example, embedded apps typically use a Meeting or Messaging space workstream).</li>
    <li><input type="checkbox"> App does not include any advertisements.</li>
    <li><input type="checkbox"> The categories you selected for the app (up to two) make sense.</li>
    <li><input type="checkbox"> Video links use https:// protocol.</li>
    <li><input type="checkbox"> The app is free of foul language and obscene images.</li>
    <li><input type="checkbox"> App benefits are described with relevant content.</li>    
</ul>

<p>

<a  id="privacy-policy"></a>

### Privacy Policy

Cisco believes privacy is a fundamental human right. Privacy statements should focus on security, transparency, and accountability. See the <a href="https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps#technical-checklist">technical checklist</a> for additional guidance.

Ensure that:

<ul>
    <li><input type="checkbox"> If requested by a customer, you can demonstrate compliance with all applicable privacy regulations and laws.</li>    
    <li><input type="checkbox"> The privacy policy is accessible and robust (see the <a href="https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps#technical-checklist">technical checklist</a> for more details on specifications).
</li>    
</ul>

<a  id="contact-information"></a>

### Contact Information

Ensure that:

<ul>
    <li><input type="checkbox"> The company name matches the contact email domain.</li>  
    <li><input type="checkbox"> The company website is valid and available.</li>
    <li><input type="checkbox"> Support URLs are valid and available.</li>
</ul>

<a  id="app-name-and-logo"></a>

### App Name and Logo

Your app name and logo must not include "Cisco," "Webex," or "Webex Meetings," or any other Cisco product names unless the app is created by Cisco Systems.

Ensure that:

<ul>
    <li><input type="checkbox"> Your app is free of any foul language and obscene images.</li>
    <li><input type="checkbox"> Your app’s name and logo are relevant to the submitted app.</li>
    <li><input type="checkbox"> Your app icon is exactly 512 x 512 px in height and width (JPG/PNG format).</li>
    <li><input type="checkbox"> Screen shots of your app are appropriate and of high quality.</li>
</ul>

## Technical Checklist

* [Secure Authentication](https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps#secure-authentication)
* [Quality Management](https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps#quality-management)
* [Privacy](https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps#privacy)
* [Design](https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps#design)

<a  id="secure-authentication"></a>

### Secure Authentication

Ensure that:

<ul>
    <li><input type="checkbox"> <strong>Accounts</strong>: Your app handles the meeting host role and meeting participant roles gracefully.</li>
    <ul>
        <li><input type="checkbox"> <strong>Your app responds with a coherent and useful error message when a command is incorrect or incorrect for the given user role.</strong></li>
        <li><input type="checkbox"> You can login as each role for your Webex org (you can use the <a href="https://developer.webex.com/docs/api/v1/roles/list-roles">List Roles API</a> to get a list of roles in your org).</li>
    </ul>
    <li><input type="checkbox"> <strong>Authorization</strong>: Your app provides the option to revoke authorization for the embedded app.</li>
    <ul>
        <li><input type="checkbox"> <strong>Once the authorization for the embedded app has been revoked, it then reroutes back to the authorization URL again before it continues to work.</strong></li>
    </ul>   
</ul>

<a  id="quality-management"></a>

### Quality Management

Ensure that:

<ul>
    <li><input type="checkbox"> Your app’s functionality matches its App Hub description.</li>
    <li><input type="checkbox"> Tests with at least two accounts (share their credentials with the Cisco team) interact with each other smoothly (when applicable).
</li>
    <li><input type="checkbox"> Your app is complete not a demo or a work in progress.</li>
    <li><input type="checkbox"> Your app doesn’t include advertisements or promotions.</li>
    <li><input type="checkbox"> Your app provides option to uninstall the embedded app (and this option works even if there is downloadable content required for the embedded app to function).
</li>
    <li><input type="checkbox"> You’ve provided the ability to re-install the app.</li>
    <li><input type="checkbox">Your app’s performance benchmarks pass regression tests. For example, apps should start within two seconds and not crash the host app or reformat a user’s disk drive.
</li>
</ul>

<a id="privacy"></a>

### Privacy

Ensure that:

<ul>
    <li><input type="checkbox"> You provide a direct https link to a PrivacyURL.</li>
    <li><input type="checkbox"> The PrivacyURL is available publicly (without needing to log into an any account).</li>
    <li><input type="checkbox"> You provide a privacy policy that explains how you handle user data.</li>
    <li><input type="checkbox"> If the privacy policy isn't available in English, you will need to send us a human-translated English version by email.</li>
    <li><input type="checkbox"> Users have the capacity to request to delete, access, and transfer an individual’s data.</li>
    <li><input type="checkbox"> Personal data that is ingested and processed is not maintained or further used unless for reasons that are clearly stated and agreed to in advance to support data privacy.</li>

</ul>


<a id="design"></a>

### Design

Ensure that:

<ul>
    <li><input type="checkbox"> Your messaging-based app meets requirements of the <a href="https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces">Embedded Apps Design and Experience Guidelines for Messaging</a>.</li>
    <li><input type="checkbox"> Your meeting-based app meets requirements of the <a href="https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings">Embedded Apps Design and Experience Guidelines for Meetings</a>.</li>
    <li><input type="checkbox"> Your app’s user interface is accessible and follows general UI considerations as outlined in the App Hub Submission Preparation Guide and Partner Guide.</li>
</ul>
