---
type: Article
title: Buttons and Cards Spaces are 5 Times Faster to Load with a 50% Lower Memory Footprint
canonical_url: https://developer.webex.com/blog/buttons-and-cards-spaces-are-5-times-faster-to-load-with-50-less-memory-footprint
content_type: blog
date: '2023-05-03'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/buttons-and-cards-spaces-are-5-times-faster-to-load-with-50-less-memory-footprint)

[Buttons and Cards](https://developer.webex.com/docs/buttons-and-cards) are integral to Webex and let you add interactivity to Webex messages. Users can interact with your app in rich new ways without ever leaving the Webex client. [Bots](https://developer.webex.com/docs/bots) and [Integrations](https://developer.webex.com/docs/integrations) can add cards to Webex spaces by including a card attachment when posting a message. Card attachments use Microsoft's [Adaptive Cards](https://adaptivecards.io/) specification to define the content of the card. The Webex clients render cards with the same look and feel across every platform, letting you focus on the content and the interaction without worrying about the presentation.

With its versatility and ever-increasing popularity of Button and Cards, Developers started creating more complex and heavy cards and extensive use of cards in Spaces made loading time of such spaces painfully slow and consumption of memory was spiking for such spaces. This was a huge bottleneck in the evolution of Button and Cards story as it was making card heavy spaces unusable sometimes on macOS, Windows and iOS.

### Memory Footprint &amp; Load time before optimization

Now that we have some background, let analyze the memory footprint and load time observed in some “card heavy” spaces before the client-side optimization.

#### Memory spikes while loading and with minimal scrolling in spaces

The following table provides some analysis on the memory footprint of card heavy spaces while loading and with minimal scrolling in spaces.

**Sample space1:** This space was operational, cards only space characterized by large cards each having ~200 labels. On Space load, Memory spiked to 452.71 MB Spike then settled at 269.35 MiB.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt457d848c10703a17/644c18ad1d4d37184e1cf73c/Fig_1.jpg)

After scrolling, Memory again spiked to 412.84 MB.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9826febdbab2e0f9/644c18db46640e0796ad494a/Fig_2.jpg)

**Sample space 2:** This space was operational, cards only space characterized by large cards each having ~200 labels. On Space load, Memory spiked to 452.71 MB Spike then settled at 269.35 MiB.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt0042f9c98fe42475/644c18f5717a360937d77b8d/Fig_3.jpg)

After scrolling, Memory again spiked to 412.84 MB.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5163314f71c979f2/644c19107f34014b36befe89/Fig_4.jpg)

#### Memory spike analysis for scrolling old card messages

The following table provides some analysis on the memory footprint of card heavy spaces with extensive scrolling to old cards in spaces. For point of reference, Webex on its launch was at 308.6MB memory usage and 6.5% CPU usage.
<table>
<tr>
<th>

**Sample space 1 (Scrolled Cards Count)**
</th>
<th>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</th>
<th>

**Memory Usage in MB**
</th>
<th>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</th>
<th>

**CPU Usage Spike (%)**
</th>
</tr>
<tr>
<td>

31
</td>
<td>

&#xa0;
</td>
<td>

602.9
</td>
<td>

&#xa0;
</td>
<td>

60
</td>
</tr>
<tr>
<td>

64
</td>
<td>

&#xa0;
</td>
<td>

685.1
</td>
<td>

&#xa0;
</td>
<td>

80
</td>
</tr>
<tr>
<td>

96
</td>
<td>

&#xa0;
</td>
<td>

925.6
</td>
<td>

&#xa0;
</td>
<td>

95
</td>
</tr>
<tr>
<td>

128
</td>
<td>

&#xa0;
</td>
<td>

1000-1200
</td>
<td>

&#xa0;
</td>
<td>

102
</td>
</tr>
<tr>
<td>

156
</td>
<td>

&#xa0;
</td>
<td>

1200-1400
</td>
<td>

&#xa0;
</td>
<td>

102
</td>
</tr>
<tr>
<td>

195
</td>
<td>

&#xa0;
</td>
<td>

1400-1600
</td>
<td>

&#xa0;
</td>
<td>

110
</td>
</tr>
<tr>
<td>

224
</td>
<td>

&#xa0;
</td>
<td>

1700-2340
</td>
<td>

&#xa0;
</td>
<td>

110
</td>
</tr>
</table>

#### Loading time for Sample spaces

**Sample space 1:** This space was operational, cards only space characterized by large cards each having ~200 labels.
*Load Time: 28 - 30 Sec on an Intel 32 GB RAM Mac machine.*

**Sample space 2:** This space was operational, cards only space characterized by medium size cards each having ~30 labels.
*Load Time: 7 - 8 Sec on an Intel 32 GB RAM Mac machine.*

### Memory Footprint and Load time after optimization

Due to memory and load time issues mentioned above, sometimes card spaces were becoming unusable due to high waiting load time and memory spikes. To solve this problem, we performed card rendering optimizations in the following categories.

#### Removed inefficiencies in intermediate views

After optimizing for inefficiencies in the card view creation process, we achieved overall memory optimization of 5-15% depending on the complexity of cards.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6f518cece8663401/644ac32e5773c9110e4529f6/buttons-and-cards-are-faster-blog-5.png)

#### On-Demand loading of cards and cache optimization

Another set of optimizations is done for the Cache optimization and On-Demand loading of cards. The major blockers were maintaining scroll view height and positioning on load and while scrolling in absence of a real card. This results in:

1. Astounding 50% memory saving and 5X faster loading of card heavy spaces.

    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc0f71dac54526ae7/644ac32fa6ac921a029a0705/buttons-and-cards-are-faster-blog-6.png)

2. No abrupt memory and CPU usage spikes during scrolling card spaces. This is achieved by rendering cards on demand and optimizing cache with purging mechanism.
