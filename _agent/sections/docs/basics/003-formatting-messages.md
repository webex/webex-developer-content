---
type: Excerpt
canonical_url: https://developer.webex.com/docs/basics
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Formatting Messages
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/basics). [Full Markdown](../../../../docs/basics.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

While working with the Webex REST API is easy, there are a few things we standardize on throughout the API, such as pagination of long result sets or HTTP response codes.

## Selected section

## Formatting Messages

Webex clients, across all platforms, can send and receive a limited form of rich text messages formatted using the [Markdown markup language](https://daringfireball.net/projects/markdown/syntax). Bots and integrations can also send rich text messages formatted with Markdown, by using the [Messages API](https://developer.webex.com/docs/api/v1/messages).

Sending formatted text is super easy using the `markdown` parameter in the [Messages API](https://developer.webex.com/docs/api/v1/messages), though only a limited set of Markdown is supported at this time. See below for examples of the formatting supported in the Webex clients.

But, before we dive into the examples below, there's an important note we need to mention about line breaks: The examples below *do not* include any JSON newline characters (`\n`) to create line breaks in Webex messages—we've left them out to focus on just the specific Markdown example. To include line breaks in your JSON message body, use standard Markdown [paragraphs and line breaks](https://daringfireball.net/projects/markdown/syntax#p) with JSON newline characters. For example, to create distinct paragraphs, use two newline characters between the paragraphs:

```text
Paragraph 1\n\nParagraph 2
```

Or, for a single break between lines, end the line with two spaces followed by a single newline character:

```text
Line 1  \nLine 2
```

#### Bold

```markdown
**Title:** Add support for multiple file uploads

**Status:** Closed
```

#### Italic

```markdown
This is *the best* launch we've had so far!
```

#### Links

```markdown
Should we try the sushi place for lunch?
- [Oh yea!](http://example.com/polls/yd242?response=yes)
- [Ewww Sushi](http://example.com/polls/yd242?response=no)
- [Not today](http://example.com/polls/yd242?response=later)
```

#### Ordered Lists

Use a number, followed by a dot or right parenthesis and then a space to create an ordered list entry.

```markdown
Priorities for the week are:
1. Collect Underpants
2. ???
3. Profit
```

#### Unordered Lists

Use a `*` or `-` followed by a space to create an unordered list entry.

```markdown
Good morning Joe Fu. Here's your todo list:
- Review that really important thing.
- Meet Jason for lunch.
- Buy a new shirt. The one you're wearing is terrible.
```

#### Sub Items in Lists

Add two spaces before the `*` or `-` for each level of indentation.

```markdown
Joe's to do list:
* Buy a new shirt.
  * With buttons.
    * And a collar!
```

#### Block Quotes

```markdown
Alice, last week you said:
> I don't care what it costs. Let's book The Chainsmokers to headline Cisco Live.

Christine from finance laughed and is now questioning our sanity.
```

#### In-Line Code

```markdown
Mike, I think the issue is with the `hasPermission` function
```

#### Fenced Code Blocks

````markdown
Hello world in golang:
```
package main

import "fmt"

func main() {
    fmt.Println("Hello, 世界")
}
```
````

### Mentions

Just like in the Webex clients, [@mentions](https://help.webex.com/p5k20o/) can be used in messages to get someone's attention in a group room. To @mention someone, use one of the following methods to specify the person or group of people:

#### Mention by Email

```markdown
Hi <@personEmail:banderson@example.com|Bobby>, your order has been processed.
```

#### Mention by Person ID

```markdown
We should get <@personId:Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY|Jose> to look at that right away.
```

#### Mention by Group

```markdown
<@all>, we have some exciting news! Please watch this space for more information...
```
