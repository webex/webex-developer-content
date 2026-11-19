---
type: Article
title: Announcing The Official Webex Postman Workspace
canonical_url: https://developer.webex.com/blog/announcing-the-official-webex-postman-workspace
content_type: blog
date: '2025-10-14'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/announcing-the-official-webex-postman-workspace)

> **Info**
>
> This blog post was co-authored with Senior Technical Leader, Arun Ganeshan



For developers working with Webex APIs, the typical starting point is the [Webex for Developers Portal](https://developer.webex.com/). It's a fantastic resource with comprehensive documentation and a handy "Try It" feature to test API calls directly in the browser. But what if you could take your API exploration and development to the next level?

Enter the official [Webex Public Workspace on Postman](https://www.postman.com/webexdev/webex-public-workspace). This curated collection of Postman resources is a game-changer for anyone building with Webex. It’s more than just a list of endpoints; it’s a complete development environment that can significantly streamline your workflow.

This blog post will explore the key advantages of using the Webex Postman collection and how it can make you a more efficient and effective Webex developer.

### Postman vs. developer.webex.com: A Better "Try It" Experience

While the "Try It" feature on the developer portal is great for quick, one-off tests, it has its limitations. Postman elevates this experience in several crucial ways:

*   **Persistent Environments:** Postman allows you to save variables, authentication tokens, and other settings in environments. No more re-entering your bearer token for every single API call. Set it once in your environment, and Postman handles the rest.
*   **Complex Workflows:** You can chain multiple API requests together to simulate real-world scenarios. For example, you can create a room, add a user to it, and then send a message, all in a sequence that can be saved and re-run with a single click.
*   **Code Generation:** Postman can automatically generate code snippets for your API requests in various languages (cURL, Python, Node.js, etc.). This is a huge time-saver when you're ready to move from exploration to building your application.
*   **Collaboration:** Postman workspaces are built for teamwork. You can share collections, environments, and test results with your colleagues, ensuring everyone is on the same page.

### The Power of the OpenAPI Specification in Postman

Since the Webex team builds their API specifications using the OpenAPI standard, when this is exported into Postman, it provides several benefits:

*   **Automatic Collection Generation:** The entire Webex API collection in the public workspace is generated directly from the official OpenAPI spec. This means it's always up-to-date and accurately reflects the current state of the APIs.
*   **Structured and Searchable:** The collection is neatly organized, with every endpoint, parameter, and request body clearly defined. You can easily search for the specific API you need and see all the required and optional parameters at a glance.
*   **Built-in Documentation:** The documentation for each API call is embedded directly within Postman, right where you need it. No more switching back and forth between your testing tool and the documentation website.

### The Importance of the Postman Public Network

By hosting their collection on the Postman Public Network, the Webex team has made it incredibly easy for developers to get started.

*   **Discoverability:** Developers can easily find the official Webex collection by searching on Postman. This increases the visibility and adoption of the Webex platform.
*   **One-Click Access:** You can "fork" the collection into your own Postman workspace with a single click. This creates a copy that you can modify and experiment with, while still being able to pull in updates from the original collection.
*   **Community and Feedback:** The public workspace fosters a sense of community. You can see how others are using the APIs, and it provides a channel for providing feedback to the Webex team.

### Other Advantages

*   **Automated Testing:** Postman has a powerful test runner that allows you to write scripts to validate the responses of your API calls. You can create a suite of tests to ensure that your integrations are working as expected.
*   **Mock Servers:** You can create mock servers in Postman to simulate the Webex APIs. This is incredibly useful for frontend development or for testing your application when you don't have a live connection to the Webex services.
*   **Monitoring:** Postman allows you to set up monitors that will run your collections at a specified interval. This can be used to check the health of the Webex APIs or to ensure that your own integrations are still functioning correctly.

### Getting Started: Your First Steps with the Webex Postman Collection

Alright, you're convinced, right? Now, let's get you hands-on with the Webex Public Workspace on Postman. It's incredibly easy to get up and running, and you'll be making API calls in minutes.

Here’s a quick guide to kick off your Webex API journey with Postman:

#### Step 1: Find the Webex Public Workspace

First things first, you need to access the Webex Public Workspace. You can do this in a couple of ways:

*   **Direct Link:** The easiest way is to use the direct link: <https://www.postman.com/webexdev/webex-public-workspace>. Just click it, and it will open the workspace directly in your Postman desktop app or web client (if you're logged in).
*   **Search in Postman:** Open your Postman application. In the top bar, you can search for "Webex Public Workspace" to find the official workspace.

Once you're in the Webex Public Workspace, you'll see a variety of collections. For our first steps, we'll focus on the "Webex Messaging" collection, as it contains the APIs we'll use for our initial tests.

#### Step 2: Fork a Collection (Make it Your Own!)

This is a crucial step! When you "fork" a collection, you're essentially creating your own personal, editable copy of it in your private Postman workspace. This allows you to experiment, modify requests, and save your work without affecting the original public collection.

*   **Locate the "Webex Messaging" Collection:** In the Webex Public Workspace, find the **"Webex Messaging"** collection and select it.
*   **Click the "Fork" Button:** Hover over the collection name or click the ellipsis (...) next to it. You should see a "Fork" button or option. Click it!
*   **Choose Your Workspace:** A dialog box will appear asking you to select the workspace where you want to fork the collection. Choose your personal workspace.
*   **Name Your Fork (Optional):** You can give your forked collection a custom name if you wish, but the default is usually fine.
*   **Select the Environment (Optional):** Select the “Webex Prod US1” environment for seamless connection to Webex servers.
*   **Hit "Fork Collection":** Confirm your choice, and Postman will create a copy in your selected workspace.

**Pro-Tip:** The "Webex Messaging" collection is a great starting point, but feel free to explore and fork other collections like "Webex Meetings" or "Webex Calling" as you dive deeper!

#### Step 3: Set Up Your Authentication Token

Remember how I mentioned simplified authentication? This is where it pays off! You'll need a Webex access token to make authenticated API calls.

*   **Get Your Webex Token:** If you don't have one already, head over to the [Webex for Developers Portal](https://developer.webex.com/). Log in with your Webex account, and it will generate a temporary bearer token for you. Copy this token.
*   **Open Your Forked Collection:** In your personal Postman workspace, navigate to the forked collection you just created (e.g., "Webex Messaging").
*   **Go to the "Variables" Tab:** Click on the name of your forked collection in the left sidebar. Then, in the main Postman window, select the **"Variables"** tab.
*   **Add Your Token:** Create a variable named `access_token`. Paste your copied bearer token from the developer portal into the **"Value"** column for this variable.
*   **Update Auth:** Change the “Auth Type” field to “Bearer Token”, and in the “Token” field type `{{access_token}}` (which tells Postman to use your variable you just created).

That's it! The collection is pre-configured to use this environment variable for all its requests, so you won't have to paste your token into every single API call.

#### Step 4: Make Your First Webex API Call!

Now for the fun part – let's make an API call!

*   **Expand Your Collection:** In the left sidebar, expand your forked "Webex Messaging" collection to see the folders and individual API requests.
*   **Choose a Simple Request:** I recommend starting with something simple and safe, like:
    *   `GET Get My Own Details` (found under the **"People API"** folder) - This is `GET /v1/people/me` and will retrieve details about your own Webex user account.
    *   `GET List Rooms` (found under the **"Rooms API"** folder) - This is `GET /v1/rooms` and will list the Webex spaces (rooms) you are a part of.
*   **Click "Send":** Select the request you want to make, and then click the blue **"Send"** button in the main Postman window.
*   **Check the Response:** If everything is set up correctly, you should see a successful response (usually a **200 OK** status) in the response pane at the bottom, along with the JSON data returned by the Webex API.

Congratulations! You've successfully used the Webex Postman Collection to make your first API call.

From here, explore other requests, chain them together, and start seeing how powerful this collection is for your Webex development.

### Conclusion

The Webex Public Workspace on Postman is an indispensable tool for any developer working with Webex APIs. It provides a rich, interactive environment that goes far beyond the basic "Try It" functionality of the developer portal. By leveraging the power of Postman, you can accelerate your development, improve the quality of your integrations, and become a more proficient Webex developer.

So, head over to the [Webex Public Workspace](https://www.postman.com/webexdev/webex-public-workspace), fork the collection, and start exploring the world of Webex APIs in a whole new way!
