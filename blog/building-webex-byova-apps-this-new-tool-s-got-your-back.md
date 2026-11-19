---
type: Article
title: Building Webex BYOVA Apps? This New Tool's Got Your Back
canonical_url: https://developer.webex.com/blog/building-webex-byova-apps-this-new-tool-s-got-your-back
content_type: blog
date: '2025-07-24'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/building-webex-byova-apps-this-new-tool-s-got-your-back)

If you're tinkering with "[Bring Your Own Virtual Agent](https://developer.webex.com/webex-contact-center/docs/bring-your-own-virtual-agent)" (BYOVA) applications for Webex, you know it's all about making Webex smarter and more automated. As you get deep into building these cool solutions, keeping your [data sources](https://developer.webex.com/create/docs/bring-your-own-datasource) in check is a big deal, especially when you're still in the development phase. Good news! We've got a new command-line tool, [webex-byods-manager](https://github.com/WebexSamples/webex-byods-manager), that's here to make that part of your BYOVA development life a whole lot easier.


 <iframe src="https://app.vidcast.io/share/embed/63e954e4-f0ae-4c20-82c3-c666cda6aad3?disableCopyDropdown=1" width="100%" height="100%" title="Webex BYODS Manager Tool" loading="lazy" allow="fullscreen;autoplay;" style="position: absolute; top:0; left: 0; border: solid; border-radius: 12px;"></iframe>


<br/>

### The BYOVA Dev Headache: Keeping Data Sources Fresh

The Webex [Bring Your Own Data Source](https://developer.webex.com/create/docs/bring-your-own-datasource) (BYODS) APIs let you connect outside data to Webex Contact Center. This is basically the engine powering the connection for your BYOVA apps. We're talking real-time interactions with clever voice virtual agents in Contact Center.

Now, to keep these BYODS hook-ups secure and working right, you've got to refresh their authentication tokens regularly. Think of it like a security check – these tokens only last at most 24 hours. If you don't, they expire, and data stops flowing. While this is super important for security, it can be a real pain when you're trying to quickly build and test stuff. Manually refreshing these things via curl or Postman can eat up your time and break your concentration.

### Meet webex-byods-manager: Your Dev Buddy

That's where the new [webex-byods-manager](https://github.com/WebexSamples/webex-byods-manager) command-line tool steps in. You can find it as a Webex Samples project on GitHub. This tool was made specifically to help developers like you handle their BYODS data sources easily while you're building.

The `webex-byods-manager` takes the headache out of refreshing data sources. You can quickly update those important tokens and settings without digging into complicated API calls or doing things by hand. This means less time messing with setup and more time actually building and refining what your virtual agent does.

Imagine you're deep into coding a new feature for your BYOVA that pulls info from some external system. If your data source token suddenly goes stale, a quick command with `webex-byods-manager` can get you reconnected and back to coding in no time. This ability to quickly refresh is a game-changer for keeping your development smooth and productive.

### Dev Tool vs. Production Powerhouse: Know the Difference

It's super important to remember that `webex-byods-manager` is a **development tool**. It's great for quick, on-the-fly management in your local setup. Perfect for a single developer or a small team moving fast on BYOVA features.

But for your actual live, production applications, you'll want something more robust, something that handles token rotation and data source management automatically and at scale. That's what the [Webex BYODS Node.js SDK](https://developer.webex.com/create/docs/sdks/byods-nodejs-sdk-introduction) is for. The SDK gives you features like custom storage, managing service app tokens, and automatically refreshing JWS tokens. It's built to give your production BYOVA apps a secure and reliable foundation. It takes care of all the tricky bits, like keeping tokens fresh and verifying them, making sure your live apps are secure and always running.

### Ready to Give It a Spin?

If you're building BYOVA apps for Webex, definitely check out `webex-byods-manager` and add it to your development toolkit. It's a simple tool that can make a big difference in how productive you are.

To get started:

- Check out the `webex-byods-manager` tool on GitHub: [https://github.com/WebexSamples/webex-byods-manager](https://github.com/WebexSamples/webex-byods-manager)
- For the real deal in production, learn about the Webex BYODS Node.js SDK: [/create/docs/sdks/byods-nodejs-sdk-introduction](https://developer.webex.com/create/docs/sdks/byods-nodejs-sdk-introduction)

Happy coding!
