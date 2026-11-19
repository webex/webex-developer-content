---
type: Article
title: How I Used ChatGPT to Build a Webex Integration
canonical_url: https://developer.webex.com/blog/how-i-used-chatgpt-to-build-a-webex-integration
content_type: blog
date: '2023-04-03'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/how-i-used-chatgpt-to-build-a-webex-integration)

One of the most powerful features of Webex is its ability to integrate with other tools and platforms. In this blog post, we'll show you how to use ChatGPT, a large language model trained by OpenAI, to generate the code for a Webex integration that receives a webhook and converts the data into an adaptive card that is posted into a Webex space by a Webex bot.

Using ChatGPT, you can generate the code needed to process the webhook data and generate an adaptive card that can display the data in a visually appealing way. You can then use this code to build your Webex integration.

Whether you're a developer looking to streamline your integration workflows or a business user looking to improve your team's productivity, this blog post will provide you with a step-by-step guide to using ChatGPT to generate the code for a powerful Webex integration. So, let's get started!

### Our Project

Our ChatGPT-generated integration will receive a webhook from an external service and process the webhook data and convert it into an adaptive card. The adaptive card will display the data in a visually appealing way and provide buttons or other interactive elements that allow users to act on the data. Once the adaptive card has been generated, our integration will use a Webex bot to post the card into a Webex space, where it can be viewed and interacted with by the appropriate team members. This integration will allow teams to quickly and easily access and act on important data from external sources within their Webex spaces, improving collaboration and productivity.

#### Webex Integrations

A Webex integration is a connection between Webex and another tool or platform that allows you to enhance the functionality of both. With a Webex integration, you can bring together the collaboration features of Webex with the data and workflows of other tools, such as project management software or customer relationship management (CRM) systems. This allows you to streamline your workflows, reduce manual data entry, and collaborate more effectively with your team. For example, you might use a Webex integration to automatically create a Webex meeting when a new project is created in a project management tool, or to automatically post updates to a Webex space when a new lead is added to a CRM system. The possibilities are endless, and building a Webex integration can help you work smarter and more efficiently.

#### Webhooks

Webhooks are a way for applications to send real-time information to other applications or services. They work by sending an HTTP request to a URL specified by the receiving application, which triggers an action based on the data contained in the request. Webhooks are commonly used to trigger automated actions, such as sending notifications or updating data in response to an event in another application.

#### Adaptive Cards

Adaptive Cards are a type of user interface (UI) component that allows developers to create interactive, data-rich cards that can be displayed in various contexts, such as in a messaging app or on a website. Adaptive Cards can be customized to display different types of data, including text, images, and interactive elements like buttons or dropdown menus. They are designed to be flexible and responsive, adapting to different screen sizes and device types.

#### Webex Bots

Webex Bots are a type of virtual assistant that can interact with users in Webex spaces. Bots can be used to automate tasks, such as sending notifications or scheduling meetings, and can be customized to perform specific actions based on user input. Webex Bots are programmable using a variety of languages, including Python and JavaScript, and can be integrated with other applications and services using Webex APIs. Bots can improve team collaboration and productivity by providing quick access to important information and automating routine tasks.

### Working with ChatGPT

Since this was my first attempt at using ChatGPT to generate code, the first thing I did was to ask ChatGPT how to be successful in having it generate code (yes, very meta, but very rewarding). Here was its response:

```text
Define the inputs and outputs: Determine what data you want to receive 
from the webhook, and how you want to display it in the adaptive card. 
This will help you specify the inputs and outputs that are needed for 
your code.

Use ChatGPT to generate the code: Once you have defined your inputs and 
outputs, you can use ChatGPT to generate the code needed to process the 
webhook data and create the adaptive card. You can do this by providing 
ChatGPT with a description of the functionality you want to implement 
and the programming language you want to use.

Test and refine the code: Once you have the code generated by ChatGPT, 
you will need to test it to ensure that it works as expected. You may 
need to make some tweaks and refinements to the code to get it working 
perfectly with your specific webhook and Webex bot.

Integrate the code with your webhook and Webex bot: Once you are 
satisfied with the code, you can integrate it with your webhook and 
Webex bot to start receiving data and posting adaptive cards in Webex spaces.
```

#### Inputs and Outputs

I decided to make our sample application receive information about rocket launches. I told ChatGPT to generate a sample webhook payload that gives information about rocket launches. Without any other prompts, this information contained the basics like launch date, launch location, and mission name. But it also gave me info that I hadn’t considered like mission patch image URL, live feed URL, and rocket payload! I now had my “input”.

For our output, I told it to generate an adaptive card with that information in version 1.3 spec since that is what Webex currently supports. It quickly printed the JSON for an adaptive card with that data. I copied the JSON and tested it in the Adaptive Card Designer, which worked perfectly!

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltfc71e5e190725254/642afd6bab116a10dd6a2d77/chatgpt-integration-2.png)

#### Generate Code

Now that I had my inputs and outputs, I asked ChatGPT to generate a python application with: “Now that we have a sample webhook and a sample adaptive card, can you write the code in python that would receive the webhook, process the data, then post the data as an adaptive card to a Webex space? Be sure to include comments since this is sample code.” I was presented with an app.py file that appeared to do exactly what I asked!

#### Test and Refine

When I ran the code, a Flask server started up and was listening on port 5000. I didn’t feel like setting up Postman, so I asked ChatGPT to generate a curl command that would send the webhook payload we generated earlier, here’s the output:

```bash
curl -X POST -H "Content-Type: application/json" -d @payload.json http://localhost:5000/webhook
```

Running the curl command, I had a couple of errors that I had ChatGPT fix. One was major: it didn’t run the app! One was the way it encoded the request body of the adaptive card which was a quick fix. I ran the application again (adding my bot token and room id) and received a message in my space!

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltfd9b72af3389a80f/642afd6bb57cb810acb7a9f2/chatgpt-integration-3.png)

Once I had the basic functionality, I knew I wanted to add a few more features. Since security is paramount at Cisco, I asked ChatGPT to load the bot’s token and room id from environment variables instead of having it hard coded. It added the `dotenv` library and now our code is more secure for open sourcing!

I also had it add a status page endpoint so that we can see the status of our bot via a web browser. It created a new `/status` endpoint and loaded the status page html via Flask’s `render_template` functionality.

### Ship It

Happy with the results, I set up a GitHub repository and was about to publish when I remembered I needed a `README.MD` file and a `.gitignore` file. Of course, I had ChatGPT generate those for me as well! They both looked great, so I included them in my repo and pushed to GitHub!

The code is now available to try out and utilize for yourself!

[https://github.com/WebexSamples/webhook-to-card](https://github.com/WebexSamples/webhook-to-card)

Check it out and give it a try. It was exciting to see how much ChatGPT knew about Webex APIs and integrations. Don’t overlook its capabilities for your next project!
