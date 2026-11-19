---
type: Article
title: The WebRTC Story – An Introduction to WebRTC
canonical_url: https://developer.webex.com/blog/the-webrtc-story-an-introduction-to-webrtc
content_type: blog
date: '2023-07-05'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/the-webrtc-story-an-introduction-to-webrtc)

This blog is an interesting story that helps in understanding the concept of WebRTC and its basics. 

[WebRTC](https://webrtc.org/) expanded as **W**eb **R**eal-**T**ime **C**ommunication, released in 2011 has been a boon to web developers who want to build streaming applications or video calling applications. In this blog, I am going to present you with a hypothetical story so that you may just understand how the WebRTC protocol works without needing any technical expertise.

### The Story

Let us begin with a short story. Long ago, there lived two shopkeeper farmers John &amp; Finch. It was a point in time when the barter system was prevalent, and money was not invented.

These shopkeepers lived in different cities across a river and the cities were connected by a rock-solid bridge. Like how the golden gate connects San Francisco City and Marin County. Finch is a very private person and has a tough time trusting people. John, on the other hand, is an overly cautious man and does not easily make deals or trust traders. He somehow gets to know about John, and he decides to make a deal with John. Therefore, he prepares a letter with a lot of information like his shop address, his name, his farm address, and other details. In this letter, he also writes an offer to John stating that he is willing to send across a couple of items that are straight out of his farm, and in exchange he wanted to know what John would be willing to send back. Finch sends this letter through one of his dependable men. He could have tried to use the budding postal system to send this across but, a man was simply his preference of sending medium.

John reads the offer sent by Finch and was impressed just by the fact that it was so detailed with various addresses, names, and other details. He verifies them and sends out a letter to Finch in the same format of addresses and names and it has the answer to Finch's offer that he is willing to accept two of the five items that Finch offered. In return, he was ready to give Finch two different items.

They happily kept trading for months. Now, John has a new product cultivated on his farm in addition to what he has already been sending. Therefore, John takes out the same format of the letter and writes a new one stating, in addition to existing things, he would like to offer one more. Finch reads it and sends out an answer stating that he agrees.

Once again, they happily keep trading for months. Now comes the hard month of winter where they cannot cultivate or move items. Therefore, Finch sends out another letter stating he cannot send anything for now. John agrees and responds with an answer saying he cannot either.

This system of sending out a letter and the other replying kept continuing, giving them good trust in each other to trade things forever.

### The Concept

What did the above story have anything to do with the WebRTC? You might be curious. Let us break the story down to know what's underneath.

The two shopkeepers are none other than the two web clients waiting to talk to each other. It could be two different browser instances from the same computer or two different browsers from two different computers too.

The golden gate bridge is nothing but a network that passes messages between one another.

The letter with all the information is the [Session Description Protocol](https://webrtchacks.com/sdp-anatomy/), or SDP. Now, let us get into the story, the two clients wanted to talk to each other but only when they trusted each other. This is where the WebRTC protocol comes into the picture.

Client A decides to interact with Client B. Therefore, it creates an SDP, this SDP will contain all the necessary information like source server address/source IP address, track codec, timing information, etc., With this, it also would have information on what it wants to share like, the audio track/video track/content track. This kind of SDP is called an **Offer**. Now, this offer is sent to Client B through a floppy disk. Client A could have used a messaging service, an email, or a Web socket to send this SDP as it is simply a string message. However, they chose the floppy disk. Let us call it simply a preferred messaging medium. As soon as Client B receives this offer, it creates another SDP that has all its information along with an answer on whether it accepts the sharing or not. This SDP is called the **Answer** and is sent back to Client A.

Once Client A receives this Answer, they share information happily with each other. Similarly, whenever there is a change in the audio track or when the audio track is muted, or when the video track is enabled, an SDP Offer is sent across to the other end and an SDP Answer is received as part of acceptance. This Offer and Answer can also happen if they want to make the session inactive.

The following is a basic diagram of how the SDP Offer / Answer mechanism works:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltcad59e12d2ba5360/64b8240b58c6c41dca8628cf/the-webrtc-story-an-introduction-to-webrtc-2.png)

I hope this article now gives a basic idea of how WebRTC works.
