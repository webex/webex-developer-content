---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Building a MindMeld Skill
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-assistant-skills-guide). [Full Markdown](../../../../docs/webex-assistant-skills-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements](002-requirements.md)

## Article introduction

The [Webex Assistant Skills SDK](https://github.com/cisco/webex-assistant-sdk) is designed to simplify the process of creating a Webex Assistant skill.

---



> **Warning**
>
> No new features are being added to Webex Assistant Skills and only skills added through May 2025 are directly supported by Cisco.

## Selected section

## Building a MindMeld Skill

When a skill is complex and needs to handle various commands that included multiple entities, the best approach is to use Natural Language Processing. **MindMeld skills** allow us to use NLP to better classify the request and extract the important information to perform what is necessary on our backend. We are not going to go very deep into how the MindMeld SDK works, but there are a lot of resources in the official [MindMeld library](https://www.mindmeld.com/) site.

The Assistant skills SDK has tooling in place for setting up a **MindMeld skill**. For that, we can use the `project init` command with the `--mindmeld` flag set. Before we can begin, we need to add the extra dependency `mindmeld` [note ensure you are using Python 3.7]:

```bash
pip install "webex-skills[mindmeld]"
```

Let's create a skill called `greeter`:

```bash
webex-skills project init greeter --mindmeld
```

The folder structure should look like this:

![File Structure](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta06159219da09ba7/617852697569022433507bb6/greeter_directory.png)

### Invoking the MindMeld Skill

With the **greeter** skill running, let's try invoking it using the SDK `skills 

` command:

```bash
$ webex-skills skills invoke greeter

Enter commands below (Ctl+C to exit)
>> hi
{ 'challenge': 'a31ced06481293abd8cbbcffe72d712e996cf0ddfb56d981cd1ff9c1d9a46bfd',
  'directives': [ {'name': 'reply', 'payload': {'text': 'Hello I am a super simple skill using NLP'}, 'type': 'action'},
                  {'name': 'speak', 'payload': {'text': 'Hello I am a super simple skill using NLP'}, 'type': 'action'},
                  {'name': 'sleep', 'payload': {'delay': 10}, 'type': 'action'}],
  'frame': {},
  'history': [ { 'context': {},
                 'directives': [],
                 'frame': {},
                 'history': [],
                 'params': { 'allowed_intents': [],
                             'dynamic_resource': {},
                             'language': 'en',
                             'locale': None,
                             'target_dialogue_state': None,
                             'time_zone': 'UTC',
                             'timestamp': 1634880182},
                 'text': 'hi'}],
  'params': { 'allowed_intents': [],
              'dynamic_resource': {},
              'language': 'en',
              'locale': None,
              'target_dialogue_state': None,
              'time_zone': 'UTC',
              'timestamp': 1634880182}}
```

As you can see, the response of a **MindMeld skill** has the same shape as a **simple skill**. It's really just the internals of the Skill that change.

### Building New Models

Since **MindMeld skills** use NLP, we need to retrain the ML models each time we modify the training data. The SDK
provides the `nlp build` command for this purpose:

```bash
webex-skills nlp build greeter
```

After running this, the models will be refreshed with the latest training data.

As usual, you can use the `--help` option to see the documentation for this command:

```bash
$ webex-skills nlp build --help
Usage: webex-skills nlp build [OPTIONS] [NAME]

  Build nlp models associated with this skill

Arguments:
  [NAME]  The name of the skill to build.

Options:
  --help  Show this message and exit.
```

### Testing the Models

Another useful command in this SDK is the `nlp process` command. It's similar to the `skills invoke` command, in the 
sense that it will send a query to the running Skill. However, the query will only be run through the NLP pipeline so
we can see how it was categorized. Let's look at an example:

```bash
$ webex-skills nlp process greeter

Enter a query below (Ctl+C to exit)
>> hi
{'domain': 'greeting', 'entities': [], 'intent': 'greet', 'text': 'hi'}
>>
```

You can see that now the response only contains the extracted NLP pieces. This command is very useful for testing
your models as you work on improving them.

As usual, you can use the `--help` option to see the documentation for this command:

```bash
$ webex-skills nlp process --help
Usage: webex-skills nlp process [OPTIONS] [NAME]

  Run a query through NLP processing

Arguments:
  [NAME]  The name of the skill to send the query to.

Options:
  --help  Show this message and exit.
```

### More About the MindMeld Skill Handler Signature

When we created our **simple skill**, our handler had the following signature:

```python
async def greet(current_state: DialogueState) -> DialogueState:
```

You can also update the handler to give you another parameter:

```python
async def greet(current_state: DialogueState, processed_query: ProcessedQuery) -> DialogueState:
```

The `processed_query` parameter will give you the `text` that was sent to the skill, the `domain` and `intent` identified
as well as the `entities` extracted from the query. This can be useful in cases where you want to use the entities as
part of the Skill logic. We'll show an example of this in the 
[Converting a Simple Skill into a MindMeld Skill](https://developer.webex.com/docs/webex-assistant-skills-guide#converting-a-simple-skill-into-a-mindmeld-skill) section.
