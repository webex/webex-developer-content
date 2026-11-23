---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/java
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Getting Started
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/java). [Full Markdown](../../../../../docs/sdks/java.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

[GitHub](<https://www.github.com/webex/spark-java-sdk>)

## Selected section

## Getting Started

This guide will get you up-and-running with the Webex Java SDK.

### Overview

* Create Webex spaces
* Post messages

### Requirements

* Java 1.6 or greater
* This SDK requires the `spark:all` [scope](https://developer.webex.com/docs/integrations#scopes)

### Step 1: Register for a Webex Account

Before using the SDK, you will need a Webex account and a
developer access token. If you haven't already, head on over to [Webex](https://teams.webex.com/) to create an account.

Once you have an account, log into this site to get your developer
access token. You will need this token to authenticate API requests from
the SDK.

### Step 2: Install the Java SDK

The Java SDK is available on [GitHub](https://www.github.com/webex/spark-java-sdk). Clone the
repository and include the source files in your Maven project.

### Step 3: Use the Java SDK

#### Create an Example Class

For this example, we'll create a very simple Example class and set the
developer access token. You'll need this token to initialize the client.

```java
import com.ciscospark.*;
import java.net.URI;

class Example {
  public static void main(String[] args) {
    // To obtain a developer access token, visit http://developer.webex.com
    String accessToken = "$YOUR_DEVELOPER_TOKEN";
```

#### Initialize the Webex Client

Initialize the client and set the endpoint to the current Webex
API.

```java
// Initialize the client
Spark spark = Spark.builder()
  .baseUrl(URI.create("https://webexapis.com/v1"))
  .accessToken(accessToken)
  .build();
```

#### Create a New Space

Let's create a space. For now this space will only have you in it. You
can always add more people later.

```java
// Create a new room
Room room = new Room();
room.setTitle("Hello World");
room = spark.rooms().post(room);
```

#### Post a Message

Now that we have a new space, let's post a message to it.

```java
// Post a text message to the room
Message message = new Message();
message.setRoomId(room.getId());
message.setText("Hello World!");
spark.messages().post(message);
```

### Full Code

Compile and run the new class to see the SDK in action. Log into Webex through one of the clients to see your new room and new message\!

Here's the full code for the example class:

```java
import com.ciscospark.*;
import java.net.URI;

class Example {
  public static void main(String[] args) {
    // To obtain a developer access token, visit http://developer.webex.com
    String accessToken = "$YOUR_DEVELOPER_TOKEN";

    // Initialize the client
    Spark spark = Spark.builder()
      .baseUrl(URI.create("https://webexapis.com/v1"))
      .accessToken(accessToken)
      .build();

    // Create a new room
    Room room = new Room();
    room.setTitle("Hello World");
    room = spark.rooms().post(room);

    // Post a text message to the room
    Message message = new Message();
    message.setRoomId(room.getId());
    message.setText("Hello World!");
    spark.messages().post(message);
  }
}
```
