---
type: Article
title: 'Look, Ma, No Hands: Using AI to Generate and Refine Webex GitHub Sample Documentation'
canonical_url: https://developer.webex.com/blog/look-ma-no-hands-using-ai-to-generate-and-refine-webex-github-sample-documentation
content_type: blog
date: '2024-12-04'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/look-ma-no-hands-using-ai-to-generate-and-refine-webex-github-sample-documentation)

While the hype train for “artificial intelligence” (which is not and never will be) has been exhausting, as a technical writer, I've found it to be a complete game-changing enhancement to my typical workflows. Your immediate question is probably, though, “John, don't you expect AI to completely eliminate your position??!!??”, to which I reply, “AHHHHAHAHHHAHAHAHAHHAHAH!” You see, like any tool, the usefulness of an AI assistant is directly correlated to the skill of the person using it (something I learned the hard way when I purchased an expensive fountain pen thinking that would magically imbue me with calligraphy talent. And then there was my attempt at shaving with a straight razor—the less said the better.). The tool most assuredly does not make the craftsperson, and if you have no idea what to ask an AI bot or how to evaluate the output, you're still working on a “garbage in; garbage out” basis (I'm **still** struggling with AI image generation and producing something that doesn't look like Hieronymus Bosch on LSD).

### How I'm Using Gen AI

That said, with some help from persons who **DO** have subject matter expertise, you can really boost your productivity even if you didn't waste years of your life in liberal arts colleges and graduate schools. Here are just a few of the ways that I've been integrating AI tools into my daily workflows:

- I review a lot of GitHub pull requests for code comments and API descriptions. Many engineers don't speak English as a first language and are usually better coders than they are writers. With a few cleverly designed prompts, they can now clean up their existing descriptions and even create new basic descriptions from scratch, up to and including markdown formatting.
- Similarly, I work in a product management organization where many of the PMs are way more technical and product-savvy than they are key feature marketeers. With some thoughtful prompting they can get excellent overviews, use cases, and comprehensive grammar *repairing* (as opposed lukewarm waffling *suggestions* that you'd get from products like Grammarly or the current incarnation of Word's Editor).
- Finally, I find tons of use with simple prompts like, “*Convert this HTML table to markdown*”, “*Check for issues with this blueprint data structure*” or “*create a brief teaser for this blog post*” that make things which would have required multiple steps or rounds of review now just a point and click exercise.

<br/>

### The Sample Code Project

With that in mind, when Ashton Jordan, one of our Engineering Technical Leaders came to me with a Python sample script he wanted to reference in our Webex Developer Portal documentation, I decided to have a go at seeing just how much work I could lay at the doorstep of both our Microsoft Copilot integrations for Visual Studio Code and Microsoft Word, as well as our own in-house ChatGPT implementation. My idea was that I'd use Copilot for evaluating and explaining the sample Python code and our in-house chat bot to produce documentation specific to Cisco workflows.

### Understanding the Application

Ashton had created a Python Flask application to demonstrate the device OAuth 2 authorization workflow. Since this application was new to me, and I had no experience with the Flask framework (and I'm also not an auth guru), I started by entering the entire sample in Microsoft Visual Code and used the Copilot **Explain This** function from the Copilot context menu:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb0adae3c7f103478/oauth-example-ai-blog-2.png)

Interestingly, because Copilot was evaluating all the aspects of the code it prompted me to install dependencies before it would generate a description. Once I'd installed the necessary modules, I repeated my request, and Copilot produced the following output in its chat panel:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte9957faf1f79c267/oauth-example-ai-blog-3.jpeg)

You'll note that Copilot generates rather verbose descriptions for anything you select by default, and that is the case for the initial run through. More on that later…

### Exploring the Functions

I then went through each block and function, using **Explain This** to generate descriptions. Here, for instance, I asked it to explain the `poll_for_access_token` function:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf073bdd5393c4fbb/oauth-example-ai-blog-4.png)

Like I mentioned at the beginning, I had no experience with Flask-based Python applications and when I noticed the decorators preceding various functions, I wasn't sure what was going on. So, I asked Copilot, and it explained how the decorators functioned in a Flask application, “*This decorator tells Flask that the function immediately following should be associated with the root URL of the web application*” along with a great deal of further details, useful if you're new to the concept:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbad8fa2cd76e6bab/oauth-example-ai-blog-5.png)

I did the same for final line, `if __name__ == "__main__": app.run(debug=True, host='0.0.0.0', port=10060)` statement at the end, discovering that it's simply a way *“…ensure that certain code is only executed when the script is run directly, rather than when it is imported as a module in another script*.”

### Refining the Application Description for a GitHub README

Once I'd answered all my questions and entertained myself by adding a few improvements (via Copilot, of course), I used further follow-on prompts such as *Reformat that response as an ordered list in markdown format* to tweak the presentation:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5fe2eb29059539c5/oauth-example-ai-blog-6.png)



> **Info**
>
> I added the Word formatting you see in all examples since that's what I'm using to produce this blog post (no judgment). At this point, Copilot for Word does **NOT** handle formatting using standard styles in a useful way. I expect that will eventually be remedied.



The above description was a bit verbose for a GitHub readme (engineers don't need to be spoon-fed basic stuff), so I decided to condense it down a bit. This was generated after selecting the entry above in Microsoft Word and using the Copilot prompt, *Generate a concise single paragraph description using bulleted points as required*:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt982bfcdbb6f12748/oauth-example-ai-blog-7.png)

I further followed that up with a request to *Describe the additional file dependencies for this Flask application* which I then cleaned up to remove irrelevant entries:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8d6b7c729ca81992/oauth-example-ai-blog-8.png)



> **Info**
>
> Again, the formatted links were added post-generation.



## Establishing Prerequisites and Dependencies

The next thing I had to do was figure out what was required as far as prerequisites and dependencies to get the application to run as expected (meaning making Copilot tell *me* what was required…).

### Install Python Modules

Copilot was able to identify the required modules and provide the pip install statements (which are pretty simple):

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt253cc9d9c9a739ca/oauth-example-ai-blog-9.png)

You'll notice Copilot also provided descriptions for each module as well, which I suppose I could have condensed as well.

### Create an Integration and Retrieve Integration Authorization Information

Ashton's application requires a back-end Webex integration to work correctly, but as expected, Copilot, was **not** able to identify that a Webex integration was required for the script to function. For this, I turned to our own in-house ChatGPT interface starting with the prompt, *Please provide step by step instructions for creating a new Webex Integration using the Webex Developer Portal, [Webex Developer Support Team](https://developer.webex.com/my-apps/new/integration)*.

Further prompt revisions included, *Revise the ordered list so it does not use unordered lists* followed by *Revise the previous response to be a single ordered list* as well as a further clarification, *Revise the previous response so it uses a single ordered list but does not include unordered lists following each ordered list entry*. While the former prompt flattened the structure somewhat, neither that nor the latter prompt accomplished exactly what I needed.

The key problem with this part of the project was updating the outdated GPT-generated procedures that referenced our web docs and applications (even though this is Cisco-hosted and trained). The initial workflow generated by our own in-house ChatGPT implementation to get to the **Create an Integration** page had to be re-worked because the generated steps were erroneous. The steps for filling out the integration page were also incomplete and had to be keystroked. After making the required corrections, I triumphantly added an introductory sentence that I wrote *all by myself*:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltaf49790ee29fd904/oauth-example-ai-blog-10.png)



> **Info**
>
> Our Webex AI Assistant is currently in beta, and, once released, it should markedly improve the accuracy of such queries.



### Run the Sample

To run the sample, all Copilot really had to say was `python oauth.py` and make sure you've got your dependencies installed. Of course, while that's technically correct, there were a few more things I needed to add, including example output:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltad94aebdca5f7a5f/oauth-example-ai-blog-11.png)

### Putting Everything Together

Once I'd finished writing, or, more appropriately, assembling, reviewing and editing, I converted the final document into Github markdown:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte92ca991452970b0/oauth-example-ai-blog-12.png)



> **Info**
>
> You can take a look at the complete project here: <https://github.com/WebexSamples/webex-device-oauth-sample>.



### Key Takeaways

There are tons of things that are best avoided when using GPT tools, including relationship advice, political analysis and generating a step-by-step guide to removing your own appendix, but an absolutely perfect use is augmenting your coding workflows. Assuming you know *what* you want to do (and that it's possible), you can get quick *working* answers to things like “*Display syntax highlighted code in a browser window*” or “*Base64 encode the output from this function*.” Relatedly, when you find something in a code base you don't understand, you can get extremely accurate explanations that you can use for documentation purposes or as a part of understanding and expanding functionality or solving issues.



> **Info**
>
> To be honest, even when something sounded like the completely wrong thing to do, it was really instructive to ask Copilot how to do it-—it often suggested solutions that didn't seem obvious at first.



As a final, note, I also recommend keeping a running list of the prompts that you use as well as the refinements, and keep testing them. You'll then have a library that you can share with team members that they can also contribute to, saving everybody time and effort.

### Need Some Help? We Got You Covered!

Remember, if you need help actually developing your application, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
