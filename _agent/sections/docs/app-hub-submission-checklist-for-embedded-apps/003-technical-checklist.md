---
type: Excerpt
canonical_url: https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Technical Checklist
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps). [Full Markdown](../../../../docs/app-hub-submission-checklist-for-embedded-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use these checklists to make sure your Embedded App is ready for submission to App Hub.

## Selected section

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
