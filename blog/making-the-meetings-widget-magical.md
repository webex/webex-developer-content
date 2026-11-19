---
type: Article
title: Making the Meetings Widget Magical
canonical_url: https://developer.webex.com/blog/making-the-meetings-widget-magical
content_type: blog
date: '2022-08-29'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/making-the-meetings-widget-magical)

Earlier in January 2022, Cisco released a new Webex Meetings Widget for React developers, enabling them to seamlessly embed Webex into their web applications. But what if you don't know React and simply want to add the widget to your existing HTML page? If you are in need of a quick way to embed Webex into your web app with just a few lines of HTML code, then you’ve come to the right place!!

In this blog, I will walk you through the Meetings Widget Code Generator and show you how to obtain the HTML code using our application to embed a pre-configured Webex Meetings Widget. If you’re not quite sure what the Webex Meetings Widget is or if you want more details about that, you can find more information in [The New Webex Meetings Widget blog](https://developer.webex.com/blog/the-new-webex-meetings-widget), but put simply – as the blog mentions, “[Webex Widgets](https://developer.webex.com/docs/widgets) provide developers with the ability to include Webex native applications features directly into their web applications with just a few lines of code”.


### Meetings Widget Code Generator

Let’s jump right into it! To generate the HTML code based on the selected (chosen) customization option, the Meetings Widget Code Generator makes use of the ‘react-code-blocks’ library. This web application requires you to input your access token and destination token. Hint: If you’re looking for the access token, it can be found [here](https://developer.webex.com/docs/getting-started#accounts-and-authentication) and the destination token can be entered using the SIP URI, email address(s), people ID(s), or room ID you’re using. Once you enter in the access token and the destination token, the meeting will be rendered on the right side of the application. It will show all the controls available for customization by default, but these can be toggled on and off, depending on your needs. Next, let’s make it yours and do some customization!

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt48f1142669f54d97/630cd7fef86a7b0f545948c3/Screen_Shot_2022-08-26_at_2.37.57_PM.png)

&nbsp;

### Extended Customization Options

What type of customization is available and how do you customize it? All the meeting controls are enabled inside the Webex Meetings Widget by default. You are then able to customize these controls by clicking the “Show Customization Options” button and de-selecting the ones you don’t want included. 
  
First, let’s get into what customization is available. This app gives you options for the layout selection, widget theme, customized width, and height settings. That’s not all! There is even an option listed as “Draggable”, which allows the end user to drag the widget around the webpage, for easy engagement and a smooth experience. With all these choices, you’ll want to know what it will look like. We took care of that too. As you continue to customize, a live preview will display your choices on the right side of the app. 
  
You will not only be able to see how everything looks in the ‘before a meeting’ preview (also known as the interstitial phase), but also how it will look during a meeting. With a live preview of each selected option, you can be certain the customization will be appropriately reflected in the HTML code! 
 
Technically speaking, by clicking “Submit”, the code generator adds the chosen controls as an array of strings and passes it as a parameter to render the embeddable Webex Meetings Widget. HTML code is then generated at the bottom for you to use! Code Generator Source code for the brave is available [here](https://github.com/wxsd-sales/meetings-widget-code-generator-demo)! 

Once you like the way everything looks and you are ready to place the widget in your web page, simply click the “Submit” button to generate your customized HTML code and copy/paste it into your app!

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta3b5e010c71b03df/630cd7fe72b92254289b0e09/Screen_Shot_2022-08-26_at_2.38.43_PM.png)

HTML code is then generated at the bottom, which you'll use to render this magical widget. Now it’s time for you to experience it for yourself! Test it out [here](https://wxsd-sales.github.io/meetings-widget-code-generator-demo/) to see what you think or take a look at the source code for this project [here](https://github.com/wxsd-sales/meetings-widget-code-generator-demo)!

### Getting Help

As always, we have a lot of great developer resources to assist along the way, whether it is needing help leveraging transcriptions in the SDK, or questions about any of the other Webex APIs:

- If you have questions on the Meetings Widget Code Generator, reach out to our team by emailing us at wxsd@external.cisco.com
- If you have a CEC login, check out this app and more on our [Webex Labs site!](https://collabtoolbox.cisco.com/webex-labs)
