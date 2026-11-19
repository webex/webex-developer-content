---
type: Guide
title: Webex API and SDK Support Policy
display_title: Support Policy
canonical_url: https://developer.webex.com/docs/webex-api-and-sdk-support-policy
content_type: documentation
product_group:
- webex-suite
categories:
- app-hub
- explore
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-api-and-sdk-support-policy)

This article outlines the current Webex API and SDK support policies.

## Versioning

Webex APIs and SDKs are versioned using standard SEMVER (<https://semver.org/>).

Version format: MAJOR.MINOR.PATCH

- Bug fixes not affecting the API increment the patch version
- Backwards compatible API additions/changes increment the minor version
- Backwards incompatible API changes increment the major version

## Current End of Life (EOL) Notices

### XML API Deprecation

- [XML API Deprecation Announcement](https://developer.webex.com/docs/webex-xml-api-deprecation-announcement)

### SOAP API Deprecation

Due to reasons of security and maintainability we are going to deprecate the recordings SOAP API. In effect Jan 1, 2023 the recordings SOAP API is being deprecated and should not be used for any new projects.
On June 30, 2023 the recordings SOAP API will be permanently shut down. This means customers have a full 6 months to migrate from the current recordings SOAP API to the alternative REST APIs.
Depending on your use cases we recommend using the [/recordings REST resource](https://developer.webex.com/docs/api/v1/recordings). Other functionality in the current SOAP API is replaced by the following APIs: [Meeting Participants](https://developer.webex.com/docs/api/v1/meeting-participants), [Meetings Chat](https://developer.webex.com/docs/api/v1/meeting-chats), [Meetings Polls](https://developer.webex.com/docs/api/v1/meeting-polls), [Meetings Q&A](https://developer.webex.com/docs/api/v1/meeting-q-and-a)

**Publish date**: 12/27/2022

## APIs and SDKs EOL Policy

### Normal Upgrade Cycle

**API** versions will be deprecated 18 months after the release of a new version.

- At the time of the new release, a notification will be sent to all customers that a new version is available including the change log of what was added or fixed.
- After 12 months customers still using deprecated APIs will be contacted with an ever increasing frequency being asked to upgrade.
- At the 18 months mark the deprecated APIs shall be switched off using 410 HTTP code.

Additions of fields to API filters (query parameters) and response fields may happen at any time and are not considered either an upgrade or a breaking change.

**SDK & Widget** versions will be deprecated 12 months after the release of a new minor version or 18 months in case of a major version.

- At the time of the new release, Cisco will communicate to the community about the changes that are included in the new version and reminders to upgrade.
- At the 18-month mark, the deprecated SDK or Widget may stop functioning. Cisco will attempt to help customer apps "fail gracefully" in such cases.
- Only releases under the latest tag will fall under the above support model.
- The Webex JavaScript SDK version 2.60.x is supported until September 30, 2025. Patches for minor or security issues will be released until this date. However, these releases will also reach End of Life (EoL) by September 30, 2025, irrespective of the date they were published.

### Priority Upgrade Policy

A **priority** upgrade will be required if there is an issue discovered that impacts Webex' ability to maintain quality of service. If a priority upgrade is required for the API or an SDK, the old versions will be supported up to 6 months from the time of release of the new version.

Occasionally we are forced to change API behavior or signature. We will announce these changes with a 4 week minimum notice on the API Change Log.
Reasons for this changes may include:

- changed security requirements
- a bug fix
- API functionality that was never supported and needs to be remove

### Critical Upgrade Policy

A **critical** upgrade will be limited to changes that are required to remediate security and/or data protection or loss issues. If a critical upgrade is required for the API or an SDK, the old versions will be immediately deprecated at the time of release of the new version.

- Connections from previous version may be refused immediately.
- At the time of the new release, a notification will be sent to all customers using the existing version that a new version is available to address a critical issue and include appropriate details of the impact of the critical issue. Instructions will be provided on how to upgrade to the new version as soon as possible with an offer of assistance from support.
- Technical support and Customer Success will work with all affected teams until upgrades are completed.

## Deprecating SDK APIs

According to SEMVER recommendations to deprecate functionality in a previously released SDK we shall:

- Update the documentation and create a guide for how to migrate to the new set of APIs.
- Issue a minor release with the APIs that are being deprecated clearly marked.
- Issue a new major release shortly after with the deprecated APIs removed.
