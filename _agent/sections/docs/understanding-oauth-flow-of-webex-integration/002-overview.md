---
type: Excerpt
canonical_url: https://developer.webex.com/docs/understanding-oauth-flow-of-webex-integration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/understanding-oauth-flow-of-webex-integration). [Full Markdown](../../../../docs/understanding-oauth-flow-of-webex-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Step 2: Registering a custom Webex integration](004-step-2-registering-a-custom-webex-integration.md)

## Article introduction

This tutorial demonstrates how to perform Webex OAuth2 authentication for a Webex Integration.

## Selected section

## Overview

[**Webex**](https://www.webex.com/products/teams/index.html) is a cloud service providing persistent chat, room-based collaboration, WebRTC video conferencing, and more. Developers can easily integrate solutions with **Webex** via the [Webex REST API](https://developer.webex.com/docs/getting-started) - for example to add **Webex** messaging features to an app user interface, or to automate sending **Webex** messages to rooms based on business system or real-world events.

![Screen Shot](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltab2659939a7af7d9/61f00ce6e30aaf137e48ca64/screenshot.jpeg)

Application developers integrating with **Webex** that wish to use OAuth/SSO for authenticating users and performing API requests on their behalf must register their app via the Cisco **Developer Portal** portal - defining the application name, permissions, and [OAuth2](https://datatracker.ietf.org/doc/html/rfc6749) redirect URL (more on this later).  During registration, the system generates a **Client ID** and **Client Secret** pair, which are later used by the application to access the **Webex** OAuth2 authentication service.  During this tutorial, you will create a new custom app registration, and generate a **Client ID** and **Secret**.

In this tutorial, we will examine a small sample HTML/JavaScript application that demonstrates how to perform a **Webex** OAuth2 authentication.  We'll walk through some of the key concepts and code details, then use the app to generate a **Webex** API access token.



> **Info**
>
> If your application does not need to 'impersonate' end users, and will only be performing **Webex** API calls on its own behalf, you may want to create a [Webex bot](https://developer.webex.com/docs/bots), and use its access token, rather than implementing OAuth.
