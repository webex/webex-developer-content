---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-quickstart
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Create Project Structure
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-quickstart). [Full Markdown](../../../../docs/cc-web-widgets-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md) [Known Issues/Limitations](010-known-issues-limitations.md)

## Article introduction

This Quickstart Guide walks you through integrating Webex Contact Center capabilities using React widgets into your application from the ground up. Follow these steps to create a fully functional application.

## Selected section

## Create Project Structure

Create a project structure as shown below.

```shell
my-cc-project/
├── public/
│   └── index.html          # HTML entry point
├── src/
│   ├── App.jsx             # Main application component
│   ├── App.css             # Main application css
│   └── index.jsx           # Application entry point
├── package.json            # Project dependencies
└── webpack.config.js       # Webpack configuration
```
