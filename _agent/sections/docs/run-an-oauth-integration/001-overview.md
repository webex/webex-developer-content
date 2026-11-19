---
type: Excerpt
canonical_url: https://developer.webex.com/docs/run-an-oauth-integration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/run-an-oauth-integration). [Full Markdown](../../../../docs/run-an-oauth-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

This tutorial shows you how to get a Node.js server running locally that acts as an OAuth client for a Webex [integration](https://developer.webex.com/docs/integrations), obtain an API access token for the authenticating user, and uses it to call a Webex API to get information about the user.

## Selected section

## Overview

This tutorial shows you how to get a Node.js server running locally that acts as an OAuth client for a Webex [integration](https://developer.webex.com/docs/integrations) using a [existing application built with Node.js and Express](https://github.com/WebexSamples/webex-oauth-integration). The app presents a button for the user to start the OAuth flow. After the user has authenticated with Webex and accepted the requested [data scopes](https://developer.webex.com/docs/integrations#scopes) they are redirected back to the Node.js app. The app obtains an API access token for the authenticated user from Webex and uses it to call the [Get My Own Details](https://developer.webex.com/docs/api/v1/people/get-my-own-details) endpoint. The user's display name is parsed from the response and displayed on the rendered HTML page. As next steps, suggestions are made for creating a new page that lists the user's spaces.

![Overview](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt79c791c28d707a47/636c28e10b52047adbb942a7/brand_new_flow.png)

The Node.js application uses [Express](https://expressjs.com/) to define HTTP routes and [embedded JavaScript templates](https://ejs.co/) (EJS) to compile and render HTML pages that contain data returned by the Webex API, such as the user's display name. HTTP calls to the Webex API are made using the [node-fetch](https://www.npmjs.com/package/node-fetch) package from NPM.
