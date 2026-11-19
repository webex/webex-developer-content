---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-and-aws-lex
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 2: Setting Up AWS Lex'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-and-aws-lex). [Full Markdown](../../../../docs/byova-and-aws-lex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

Transform your contact center with intelligent voice interactions using Webex Contact Center's BYOVA (Bring Your Own Virtual Agent) feature and AWS Lex.

## Selected section

## Step 2: Setting Up AWS Lex

### 2.1 Sign in to your AWS account

1. Sign in to the AWS Management Console and open the Amazon Lex console at <https://console.aws.amazon.com>.

### 2.2 Create Your AWS Lex Bot

You can create a bot with Amazon Lex V2 in multiple ways. If you want to learn more about all the ways, refer to [this](https://docs.aws.amazon.com/lexv2/latest/dg/create-bot.html) guide.

In this section, you create an Amazon Lex bot (BookTrip).

1. Sign in to the AWS Management Console and open the Amazon Lex console at https://console.aws.amazon.com/lex/.

2. On the **Bots** page, choose **Create**.
3. On the **Create your Lex bot** page,
   - Choose **BookTrip** blueprint.
   - Leave the default bot name (BookTrip).
4. Choose **Create**. The console sends a series of requests to Amazon Lex to create the bot. Note the following:

5. The console shows the BookTrip bot. On the **Editor** tab, review the details of the preconfigured intents (BookCar and BookHotel).

6. Test the bot in the test window.

If you would like to use generative AI to optimize LexV2 bot creation and performance, please refer to this [guide](https://docs.aws.amazon.com/lexv2/latest/dg/generative-features.html)

If you wish to use AWS Bedrock Agents with a custom knowledge base—as part of your autonomous bot workflow, here are some guides that can help you [setup agents](<https://docs.aws.amazon.com/bedrock/latest/userguide/agents.html>) and [knowledge base](<https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base-create.html>)


### 2.3 Lex Bot Configuration & Testing

Once you have successfully created the Lex bot following the documentations provided above, please make sure to add Agent Intent to your bot.

1. Sign in to the AWS Management Console and open the Amazon Lex console at <https://console.aws.amazon.com/lex/>.

2. From the list of bots, choose the bot that you created, then from **Add languages** choose **View languages**.

3. Choose the language to add the intent to, then choose **Intents**.
4. Choose **Add intent**, give your intent a name, and then choose **Add**.
5. Add **Sample Utterances**

   ```text
   Agent
   Can I talk to an agent
   Can I talk to a person
   Representative please
   Connect me to a person
   ```

   Feel free to add or remove utterances, but please keep it specific to the agent

6. Set up **Fulfillment** response
   - On successful fulfillment

     ```text
     Okay, transferring you to a human agent.
     ```

   - In case of failure

     ```text
     I'm sorry, but I couldn't connect you to a human agent. Please try again.
     ```

After creation, test your bot inside the AWS Lex UI and ensure that all basic and agent-related intents work as expected.

### 2.4 Collect Lex Bot Identifiers

Once your bot is ready, note the following identifiers:

- Bot name
- Bot ID
- Bot alias name
- Alias bot ID

You will enter these into your Webex Lex connector configuration.

### 2.5 IAM Policy and Permissions

To allow Lex and its integrations to function, attach these managed policies to your IAM user:

- AmazonLexFullAccess
- AmazonPollyReadOnlyAccess (required for text-to-speech features)​

For Bedrock/advanced integrations, you may to add extra policies. Please refer to this [documentation](https://docs.aws.amazon.com/lexv2/latest/dg/bedrock-agent-intent-permissions.html) to learn more.

### 2.6 Create access keys

1. Use your AWS account ID or account alias, your IAM user name, and your password to sign in to the [IAM console](https://console.aws.amazon.com/iam).

2. In the navigation bar on the upper right, choose your user name, and then choose **Security credentials**.

3. In the **Access keys** section, choose **Create access key**. If you already have two access keys, this button is deactivated and you must delete an access key before you can create a new one.

4. On the **Access key best practices & alternatives** page, choose your use case to learn about additional options which can help you avoid creating a long-term access key. If you determine that your use case still requires an access key, choose **Other** and then choose **Next**.

5. (Optional) Set a description tag value for the access key. This adds a tag key-value pair to your IAM user. This can help you identify and update access keys later. The tag key is set to the access key id. The tag value is set to the access key description that you specify. When you are finished, choose **Create access key**.

6. On the **Retrieve access keys** page, choose either **Show** to reveal the value of your user's secret access key, or **Download .csv file**. This is your only opportunity to save your secret access key. After you've saved your secret access key in a secure location, choose **Done**.

Please save this Access Key and Secret Access Key very safely.

---
