---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-and-aws-lex
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Prerequisites
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-and-aws-lex). [Full Markdown](../../../../docs/byova-and-aws-lex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Transform your contact center with intelligent voice interactions using Webex Contact Center's BYOVA (Bring Your Own Virtual Agent) feature and AWS Lex.

## Selected section

## Prerequisites

Before starting, ensure you have:

- **Webex Account**: A Webex account (create one at [webex.com](https://webex.com) if needed)
- **Webex Contact Center Access**: Either:
  - Follow Step 1 to request a sandbox (recommended for first-time users)
  - OR have existing access to a Webex Contact Center organization with BYOVA feature enabled

- **AWS Account**: An active AWS account with appropriate permissions
- **Development Environment**:
  - Python 3.8 or higher
  - Git
  - Terminal/Command Prompt access
- **Gateway Hosting**: You'll need a public HTTPS URL for your gateway:
  - **For Testing**: Use [ngrok](https://ngrok.com) (free tier available) - covered in Step 3
  - **For Production**: Prepare a public domain with HTTPS (AWS, Azure, GCP, or on-premises)
  - **Note**: You'll configure this URL in Step 3 and use it throughout Steps 4-5

- **Basic Knowledge**: Familiarity with:
  - Webex Contact Center concepts
  - AWS services (Lex, IAM)
  - Python development
  - gRPC and REST APIs

---
