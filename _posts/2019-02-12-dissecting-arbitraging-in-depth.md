---	
layout: post
date: 2019-02-12 01:00
title:  "Dissecting Arbitraging.co in-depth— you’ve been scammed (again)?"
mood: happy
category: 
- docs
---


<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/2600/1*HFTNgb-w4qfMBtVmfNu2Ag.png" />
  <figcaption>Photo by <a href="https://unsplash.com/rmaedavis" target="_blank">Rachel Davis</a>.</figcaption>
</figure>


### [UPDATE]
> This post was initially posted on [Medium](https://medium.com/@0xf3d/dissecting-arbitraging-co-in-depth-youve-been-scammed-again-21306de00fe5) (archived [here](https://web.archive.org/web/20190124114926/https://medium.com/@0xf3d/dissecting-arbitraging-co-in-depth-youve-been-scammed-again-21306de00fe5) ) on 21 January 2019 and shadow banned from Medium on 7 February 2019. I suspect my original post was been *brigaded*, a practice of upvoting/downvoting/reporting content to have it removed.

<!--more-->

<figure class="aligncenter">
  <img src="https://i.imgur.com/3rwayzF.png" />
  <center><figcaption>Stats of the original post from my Medium dashboard</figcaption></center>
</figure>



### DISCLAIMER

> *All information shared in this blog-post were collected from public sources with
> different OSINT techniques not discussed in depth here. I won’t disclose all of
the information collected during these months but only a significant part
considered relevant for the readers.*
>
> **The views expressed in this article are my own and do not necessarily reflect
> the view of other people***.*
>
> *Crypto space is insane right now and strongly unregulated so if you’re not quite
> confident with something, question yourself, doubts everything and DON’T EVER
trust random people that promise you easy gains.*

*****

### Introduction

According to an [article](https://www.forbes.com/sites/oliversmith/2018/07/24/how-to-verify-an-ico-isnt-a-con-scams-scoundrels-and-multimillion-dollar-frauds/) appeared on Forbes the Initial Coin Offering ([ICO](https://en.wikipedia.org/wiki/Initial_coin_offering)) market was expected to be worth more than **$20 billion** **in 2018**. In fact, in just a few years, thousands of high-tech investors have flooded the sector with cash, hoping to get in early on the next hot crypto token.

**Initial Coin Offering**, for people who are not familiar with, is a new form of crowdfunding where the investors can send money in order to support a project. The main difference between ICOs and crowdfunding are the money accepted from the investors: on ICOs only cryptocurrencies are allowed and the most common currency used is [Ethereum](https://coinmarketcap.com/currencies/ethereum/), the second largest cryptocurrency in terms of market cap at the time of writing. Instead, for every Ether (or fraction thereof) sent to the company wallet, a “[smart contract](https://en.wikipedia.org/wiki/Smart_contract)” would automatically send back a different type of money, typically a token (referred as [ERC-20](https://en.wikipedia.org/wiki/ERC-20) on Ethereum blockchain), that would give people special access to the platform plus act as equity in the network.

But, as in any market growing this fast, the number of scams and fraudsters preying on unsuspecting investors are also growing by the day. Moreover, unlike an Initial Public Offering ([IPO](https://en.wikipedia.org/wiki/Initial_public_offering)) — where stock exchanges dictate strict rules around the disclosure and the auditing a company must go through — ICO scams run rampant as the **fundraising method is largely unregulated**.

Moreover, a recent [study](https://research.bloomberg.com/pub/res/d28giW28tf6G7T_Wr77aU0gDgFQ) revealed that **approximately 78% of ICOs conducted in 2017 were identified as scams**.


<figure class="aligncenter">
  <img src="https://i.imgur.com/dE7Qlgd.png" />
  <center><figcaption>Listed Coins/Tokens (in $M USD), $50M+ Market Cap (source: Satis Research)</figcaption></center>
</figure>

In this massive amount of scamming going on, in July 2018 a specific platform has been drawn to my attention: this platform was called **Arbitraging**.

This platform is available on [https://arbitraging.co](https://arbitraging.co/) but I made several snapshots during 2018 on [WaybackMachine](https://web.archive.org/web/20180715000000*/arbitraging.co) in case it will get deleted, changed or whatever.

### What is Arbitraging.co?


<iframe width="560" height="315" src="https://www.youtube.com/embed/TRt0ZBhFXXs" frameborder="0" allowfullscreen></iframe>

According to their presentation video, **Arbitraging.co** is a **revolutionary arbitrage trading platform that operates on crypto markets**.

For people who are not familiar with, *Arbitrage is the simultaneous purchase and sale of an asset to profit from an imbalance in the price*, or better, *it is a trade that profits by exploiting the price differences of identical or similar financial instruments on different markets or in different forms*.

<figure class="aligncenter">
  <img src="https://i.imgur.com/IluP9wo.png" />
  <center><figcaption>A graphic example of an arbitrage trade.</figcaption></center>
</figure>

This concept can be easily transferred also in the cryptocurrencies world since multiple exchanges offered the same cryptocurrencies (or token) at different prices: **if you're able to exploit this price difference you made profits**. Simple as that.

So **why this platform claim to be revolutionary** since arbitrage is a well-known technique?

Because they implemented a piece of software, called **aBOT**, that can automatically find and trade Arbitrage opportunities where you can make a profit instantly and, according to their [whitepaper](https://www.arbitraging.co/index_files/docs/Whitepaper_EN.pdf) (archived [here](https://web.archive.org/web/20190110185121/https://www.arbitraging.co/index_files/docs/Whitepaper_EN.pdf)) “you will only be paid from the revenue generated by the aBOT and this make Arbitraging **a long term sustainable project**.”


<figure class="aligncenter">
  <img src="https://media.giphy.com/media/cAhFws5mOvxRp37OZp/source.gif" />
</figure>

I think that **this is not going to happen** and touting these high-returns as the primary benefit of the project is also a bad sign of an unclear business going on.

*****

## Dissecting the Arbitraging bots

Arbitraging, like many other ICOs in these last years, didn’t bring any piece of innovation except an **unknown mysterious trading bot** that is used to exploit the crypto market price volatility through arbitrage trades.

So why an automated bot armed with big bags of cryptocurrencies on this current market will fail?

The answer is **slippage**.

<figure class="aligncenter">
  <img src="https://i.imgur.com/SnQ6vst.png" />
  <center><figcaption>https://www.investopedia.com/terms/s/slippage.asp</figcaption></center>
</figure>

**Slippage** refers to the difference between the expected price of a trade and the price at which the trade is actually executed and this difference is more noticeable in high-volatility markets, e.g. cryptocurrencies.

So a couple of scenarios of what could do Arbitraging with their investors' money instead of filling them on a trading bot that clearly can’t be designed to “[never make a loss](https://www.youtube.com/watch?v=TRt0ZBhFXXs)”: (**these scenarios are assumptions of the author and not confirmed by any evidence**)

* they manually try to exploit some arbitraging opportunities in various
cryptomarkets
* they day-trade with massive sums using whale techniques such as [pump&dump scheme](https://theoutline.com/post/3074/inside-the-group-chats-where-people-pump-and-dump-cryptocurrency?zd=1&zi=dmmrhvqa) or [flash crashes](https://thenextweb.com/hardfork/2018/12/06/coinbase-ethereum-price-collapse/) on unregulated markets
* worse things

My own thinking on this story is that **the claimed bot does not exist**, or it does not perform as they claim and with this blog-post and **I’ll show you some evidence** about this shady organization, their YouTube promoters, their members and the community correlated with evidence found.

Once you register a new account (temporary email addresses accepted and no ID required) you’re able to join the **Arbitraging trading platform**.

<figure class="aligncenter">
  <img src="https://i.imgur.com/kWj2dC6.png" />
  <center><figcaption>Arbitraging dashboard once logged in.</figcaption></center>
</figure>



*****

## Dissecting the guaranteed passive income

Let’s have a look of the **aBOT dashboard** below but don’t pay too much attention to all the values shown such as *“arb price in aBOT”* or *“stop price”*. These terms are hidden fees and other mechanisms added during 2018 to trick the investors in order to lock their funds.

The most underrated values here are the indicated daily profits in the **aBOT Payout History Graph**, on the bottom, and it shows the average returns from the aBOT: **from 0.5% up to 1.0% per day**.

<figure class="aligncenter">
  <img src="https://i.imgur.com/kWj2dC6.png" />
  <center><figcaption>aBOT dashboard: on the bottom the daily profits in the last days (up to 1%
daily). Source: arbitraging.co</figcaption></center>
</figure>


Why these numbers are **insanely high** and **clearly unsustainable**? Let’s clear this up with a simple example:

* put **$1,000** on aBOT with **100%** daily reinvest
* lock the investment for **3 years**
* an average daily return set to **0.7%** (it seems reasonable according to the history graph shown above)

This is the crazy result:

<figure class="aligncenter">
  <img src="https://i.imgur.com/xOHhq54.png" />
  <center><figcaption>$1,000 in aBOT with 100% daily reinvest turns to **$2,075,205.11** in barely 3
years. Source: https://compoundhyip.com/ </figcaption></center>
</figure>

aBOT turns your $1,000 investment in $2,075,205.11: congrats, you’re a millionaire. ❤

Without. Doing. Nothing. Just lock your initial investment and let the aBOT do its job for you.


<figure class="aligncenter">
  <img src="https://i.imgur.com/XWwtjVT.gif" />
  <center><figcaption></figcaption></center>
</figure>

**These pieces of evidence shown were already enough to identify a potential Ponzi scheme.**

According to [Wikipedia](https://en.wikipedia.org/wiki/Ponzi_scheme):

> A **Ponzi scheme** ([/ˈpɒnzi/](https://en.wikipedia.org/wiki/Help:IPA/English); > also a **Ponzi game**)[[1]](https://en.wikipedia.org/wiki/Ponzi_scheme#cite_note-1) is a form of fraud which lures investors and pays profits to earlier investors by using funds obtained from more recent investors.[[2]](https://en.wikipedia.org/wiki/Ponzi_scheme#cite_note-2) The victims are led to believe that the profits are coming from product sales or other means, and they remain unaware that other investors are the source of profits. A Ponzi scheme is able to maintain the illusion of a sustainable business as long as there continue to be new investors willing to contribute new funds, and as long as most of the investors do not demand full repayment and are willing to believe in the non-existent assets that they are purported to own.

But I got more.

*****

## A little bit of history: from XRPC to ARB

Arbitraging is just a rebranding of another platform called **XRPC** and this is not to be confused with the well-know [Ripple XRP](https://coinmarketcap.com/it/currencies/ripple/). Moreover, Internet Archive still holds a couple of copies of [it](https://web.archive.org/web/20171214153226/http://xrpconnect.co/).

<figure class="aligncenter">
  <img src="https://i.imgur.com/lDtHKed.png" />
  <center><figcaption>Interview with David Peterson CEO of Arbitraging. Source: https://www.youtube.com/watch?v=xBtUEPRoVwY</figcaption></center>
</figure>



According to this [article](https://steemit.com/xrpc/@okane81/xrpconnect-by-the-bitconnect-early-investor) (archived [here](https://web.archive.org/web/20190112123027/https://steemit.com/xrpc/@okane81/xrpconnect-by-the-bitconnect-early-investor)), XRPC was *a new protocol to serve and optimize bank transactions* and their mission was to make every effort **to ensure a high ROI** after their ICO.

**So** **why they rebranded the name to Arbitraging**? What was wrong with the XRPC name? Initially, it makes nonsense until the following table extracted from the initial XRPC whitepaper was found:


<figure class="aligncenter">
  <img src="https://i.imgur.com/mkH7wLg.png" />
  <center><figcaption>Image extracted from the original XRPC whitepaper (and properly edited).</figcaption></center>
</figure>



Ok, wait, the “**C**” on the XRP**C** name stands for “**Connect**”? And they were really comparing themselves with **Bitconnect** ([the biggest exit-scam in cryptocurrency](https://thenextweb.com/hardfork/2018/01/17/bitconnect-bitcoin-scam-cryptocurrency/)) and **ETHConnect** ([a less-know scam](https://coinclarity.com/spotting-a-scamcoin-ethconnect/))?

That’s one of the worst marketing strategies ever.

In fact, comparing both the whitepapers of XRPC and Arbitraging, a lot of similarities can be spotted as shown:

<figure class="aligncenter">
  <img src="https://i.imgur.com/UVlsTmD.png" />
  <center><figcaption>XRPC and Arbitraging whitepapers comparison</figcaption></center>
</figure>


At that time I started hearing an “[hey hey heeeey](https://www.youtube.com/watch?v=xK3yuxrmCac)” in the background.


<figure class="aligncenter">
  <img src="https://i.imgur.com/bDsTCRs.png" />
  <center><figcaption>Carlos Matos: the most (in)famous BitConnect speaker</figcaption></center>
</figure>



*****

## Dissecting the whitepaper

Arbitraging [whitepaper](https://www.arbitraging.co/index_files/docs/Whitepaper_EN.pdf), archived [here](https://web.archive.org/web/20190110185121/https://www.arbitraging.co/index_files/docs/Whitepaper_EN.pdf), is extremely vague, full of buzzwords and images and usually if there isn’t an in-depth explanation of how the technology works or how the project is going to be implemented, it’s a bad sign.

A couple of **red flags** found:

* Poor grammar
* Explicit sentences such as “We do NOT have a Multi-Level Marketing or Ponzi
structures”. Is it really worth mentioning such things?
* Price prediction of the ARB token. It’s written that the ARB token in Q4 2018
will be $200 thanks to the “ARB low total supply combined with their BOT
software”. How can they predict the token value in the near future? Short
answer: they can’t. **Don’t ever invest in an ICO simply because the company
claims their coin will increase in value.**


<figure class="aligncenter">
  <img src="https://i.imgur.com/nGpe0l7.png" />
  <center><figcaption>ARB value at the time of writing (January 2019). Source: CoinMarketCap</figcaption></center>
</figure>


* Improper use of terms and too many buzzwords such as **decentralized**,
**sustainable**, **profits**, **complete** **control**, **transparency**, etc..
* Unclear roadmap with extremely vague goals, as shown below

<figure class="aligncenter">
  <img src="https://i.imgur.com/ZuqNvzp.png" />
  <center><figcaption>Arbitraging roadmap. Source: whitepaper</figcaption></center>
</figure>



*****

## Dissecting the team

On one of the [previous](https://web.archive.org/web/20180425110700/https://www.arbitraging.co/) homepages of Arbitraging, the following team members were shown:


<figure class="aligncenter">
  <img src="https://i.imgur.com/mPh7T3o.png" />
  <center><figcaption>Arbitraging team members (old homepage). Source: https://web.archive.org/web/20180425110700/https://www.arbitraging.co/</figcaption></center>
</figure>

But at the end of 2018, a new homepage was deployed and **the team’s members
disappear** without an official statement of the company:


<figure class="aligncenter">
  <img src="https://i.imgur.com/H9c2kh5.png" />
  <center><figcaption>Arbitraging current homepage (January 2019). Source: arbitraging.co</figcaption></center>
</figure>


A couple of comments on them:

* shady backgrounds (and unconfirmed by anyone trustable in the blockchain or financial areas)
* altered or stretched low-quality images
* insufficient online presence

Moreover, back in August 2018, **another potential red flag** was disclosed:

<figure class="aligncenter">
  <img src="https://i.imgur.com/rhyowd5.png" />
  <center><figcaption>The team member Adeel Khan changes his name in Majaz Elahi</figcaption></center>
</figure>

As you can see, the CTO changed his name from *Adeel Khan* to *Majaz Elahi* and
after that, the same person was also spotted on **another shady crypto platform** called **Visus.co**.


<figure class="aligncenter">
  <img src="https://i.imgur.com/UkX8rio.png" />
  <center><figcaption>Majaz Elahi is also a member of Visus.co, another shady crypto platform. Source: http://www.visus.co/</figcaption></center>
</figure>

If you need more details about these changes, check out my following [tweets](https://twitter.com/f3d__/status/1033349771329720326) about it.

**But recently**, on 9th January 2019, in their official Telegram channel ([t.me/arbofficial](https://t.me/arbofficial)) a new photo of their dev team appeared:

<figure class="aligncenter">
  <img src="https://i.imgur.com/Wchb7c7.png" />
  <center><figcaption>Arbitraging new developers team (January 2019). Majaz appears on the right. Source: Telegram</figcaption></center>
</figure>


As you can see, **Majaz is still there** with a bunch of new faces in a tiny office and I was able to track down a potential location by finding Majaz on social media: **Lahore (Pakistan)**.

<figure class="aligncenter">
  <img src="https://i.imgur.com/NrWX2hm.png" />
  <center><figcaption>Majaz seems to be located in Lahore, Pakistan. Source: Facebook</figcaption></center>
</figure>

Since **Arbitraging community communicate only on their Telegram groups** I tried to reach them out and kindly ask a couple of questions:

* Where the office of Arbitraging is currently located? Pakistan, maybe?
* Why the team is changed? Where I can find an official statement published by Arbitraging about this changing?

In the next picture will be shown a couple of answers that I receive back. A little bit of context first: “**Anna Jo**” is an admin of their groups meaning that he/she can ban users, clear “uncomfortable” questions, etc..

<figure class="aligncenter">
  <img src="https://i.imgur.com/zAvNX3C.png" />
  <center><figcaption></figcaption></center>
</figure>

And after a couple of minutes and a couple of more questions, **I was banned from their channel**.

<figure class="aligncenter">
  <img src="https://i.imgur.com/g0A3Ur3.png" />
  <center><figcaption>Banned from an Arbitraging Telegram group.</figcaption></center>
</figure>


**This is how it works inside their community**: if you doubt something or if you trying to get more information or transparency on something you will be called out for [FUDDING](https://www.reddit.com/r/Bitcoin/comments/2dp4vh/what_is_fud/) and banned from the group. I saw numerous users been banned for simply asking questions.

*****

## Dissecting their BVI business licence

On 11 January 2019, **Arbitraging made a huge mistake** by releasing the following government document that testimony their business activities.

<figure class="aligncenter">
  <img src="https://i.imgur.com/YBP96PY.png" />
  <center><figcaption>BVI business license of Arbitraging published on 11 January 2019. Source: https://www.arbitraging.co/images/License.PNG</figcaption></center>
</figure>


Since a couple of months, **Arbitraging moved its registered office** from Singapore (initial location) to British Virgin Island (current location) and now it seems that they are fully registered and they can operate in full compliance with local laws.

Since there’s a **licence n°** on this document I verified its authenticity in the official portal of the [British Virgin Islands — Financial Services Commission](http://www.bvifsc.vg/certificate-validation) and this was the result:

<figure class="aligncenter">
  <img src="https://i.imgur.com/Tplm1fz.png" />
  <center><figcaption>The BVI business licence of Arbitraging seems not valid: Source: http://www.bvifsc.vg/certificate-validation</figcaption></center>
</figure>


More confirms are needed so I reached out the **Financial Services Commission** of British Virgin Island by email and surprisingly, a couple of hours later, **they emailed me back with a clear statement**:

<figure class="aligncenter">
  <img src="https://i.imgur.com/QVHYOry.png" />
  <center><figcaption>BVI FSC confirms: the Arbitraging business licence is not authentic.</figcaption></center>
</figure>


Not only **they confirm that this license is not authentic**, but **they’re also asking to provide them with more details about the source of this document**.

I was like:

<figure class="aligncenter">
  <img src="https://i.imgur.com/MDjTqtE.gif" />
  <center><figcaption>It really was Saturday that day, btw.</figcaption></center>
</figure>

But yes, **I sent them more details** and they kindly appreciated it:

<figure class="aligncenter">
  <img src="https://i.imgur.com/BYq6kz5.png" />
  <center><figcaption>BVI FSC BVI FSC response to other details provided</figcaption></center>
</figure>

And **after 5 days the license disappeared** from the Arbitraging website and the following message came out on their Telegram groups:

<figure class="aligncenter">
  <img src="https://i.imgur.com/6C5qdNw.png" />
  <center><figcaption>The BVI business licence was removed on 16th January 2019. Source: Telegram.</figcaption></center>
</figure>

But there is more.

On 18th January 2019, the British Virgin Island Financial Service Commission (the “FSC”) also made a [public statement](http://www.bvifsc.vg/publications/global-world-technology-limited) about this fake business license:

<figure class="aligncenter">
  <img src="https://i.imgur.com/NZMiUTq.png" />
  <center><figcaption>British Virgin Island FSC official statement. Source: http://www.bvifsc.vg/publications/global-world-technology-limited</figcaption></center>
</figure>


*****

## Dissecting their marketing: (paid?) YouTube promoters

<figure class="aligncenter">
  <img src="https://i.imgur.com/CwK9zSG.png" />
  <center><figcaption>Some of the Arbitraging YouTube promoters: Crypto Austin, Crypto Batman, Bitsaway1, Revolution in Crypto. Source: YouTube</figcaption></center>
</figure>


During these months a lot of their YouTube promoters were analyzed **in order to gain more information about them and about Arbitraging** thanks to multiple errors they made. But before that, a few points shared between those promoters:

* no financial or blockchain backgrounds provided
* very misleading video titles to obtain more investors by showing Arbitraging as a sustainable passive income platform that can make everyone rich without any types of effort
* shared connections with other well-known crypto scams (e.g. DavorCoin, ETHconnect, Visus, BitBliss Coin, FineCoin, LoopX, FineCoin, Monetize.. to name a few)

The following list identifies the most influential Arbitraging promoters.

**Crypto Batman**

<figure class="aligncenter">
  <img src="https://i.imgur.com/MjzknAE.png" />
  <center><figcaption>Blake S. aka Crypto Batman</figcaption></center>
</figure>


[Crypto Batman](https://www.youtube.com/channel/UCmA5Mi6WErJuefZOw6SM_jg) (archived [here](http://archive.is/a9wkV)) is one of the main promoters and he’s also referring himself as **ArbWarrior**: he’s a true believer of Arbitraging.

But, from time to time, he also posts videos about his disappointment when things were not going as he wanted to (e.g. withdraws delays, new updates not correctly announced, …). The point is that **he also changes his mind very frequently** and when it happened, he used to delete immediately those uncomfortable videos.

During one of this “negative” video, I was able to reach out one of their Telegram admin called **Marcus Mitchell** and ask him why Crypto Batman was very aggressive against Arbitraging. Clearly, the day after this video was gone.
¯\\\_(ツ)\_/¯

<figure class="aligncenter">
  <img src="https://i.imgur.com/3hwIUVR.png" />
  <center><figcaption>Marcus Mitchell: one of Arbitraging Telegram admin talking about Crypto Batman. Source: Telegram chat</figcaption></center>
</figure>

**Crypto County Boy**

<figure class="aligncenter">
  <img src="https://i.imgur.com/3ywnIQl.png" />
  <center><figcaption>Daniel W. aka Crypto Country Boy</figcaption></center>
</figure>



[Crypto Country Boy](https://www.youtube.com/channel/UCi1V9r8jIE06oX5J0Tcq4ow/videos) is also a major promoter of the Arbitraging platform. During [one of his videos](https://www.youtube.com/watch?v=WMGbh5TDZyA) (archived [here](http://archive.is/EmgyV)), he also showed the new upcoming UI for Arbitraging but he naively exposed an URL:

<figure class="aligncenter">
  <img src="https://i.imgur.com/TjouUgw.png" />
  <center><figcaption></figcaption></center>
</figure>


I archived a [copy](https://web.archive.org/web/20181210183727/http://arb.eugence.com/arb/arb/) in case it goes offline. Needless to say that it was a fake frontend created ad-hoc and probably purchased it on [Zenith Script Store](https://zenithscript.info/) where cheap templates can be bought for your scammy ICO platform.

<figure class="aligncenter">
  <img src="https://i.imgur.com/qNbdi7I.png" />
  <center><figcaption>The template used on the new Arbitraging UI. Source https://zenithscript.info/Ico-script/Best-Ico-script-with-lending-exchange-with-latest-design</figcaption></center>
</figure>


Uh, and by the way, **this UI has never been deployed**. Will be in the future? Who knows. ¯\\\_(ツ)\_/¯

Crypto Country Boy at the end of 2018 also starts his “own” company called [Coin.Lotto](https://www.youtube.com/channel/UCGSocRUCylcmdmBsSg3EwTg) and self-proclaimed himself as the CEO but **again he made the same error** exposing the URL of this unreleased project. I archived a [copy](https://web.archive.org/web/20190110110144/http://3.16.18.193/) in case it goes offline so you can go and have a look of this new revolutionary gambling platform.

**Note for the readers:** at the time of writing Coin.Lotto is not live yet.

<figure class="aligncenter">
  <img src="https://i.imgur.com/4IdrpTn.png" />
  <center><figcaption>URL of Coin.Lotto exposed by Crypto Country Boy. Source:
https://www.youtube.com/watch?v=pOL11SUvT_w</figcaption></center>
</figure>

But in the meanwhile, other YouTube promoters (already involved in Arbitraging) start supporting Coin.Lotto too such as [Adam Hole](http://archive.is/ni4Pq), [Crypto Clover](http://archive.fo/6sfnB), [Matty Crypto](http://archive.fo/iFsrz), etc..

**Crypto Soldier**

<figure class="aligncenter">
  <img src="https://i.imgur.com/4zjbLN4.png" />
  <center><figcaption>Marko S. aka Crypto Soldier</figcaption></center>
</figure>

**Marko S.** aka Crypto Soldier actively promoted Arbitraging. Actually, he didn’t make a lot of videos on his YouTube channel, but **he’s clearly very close to David Peterson**, the CEO of Arbitraging. He also went to David’s home and make a short video as proof.

<figure class="aligncenter">
  <img src="https://i.imgur.com/GfNfwbN.png" />
  <center><figcaption>Crypto Soldier (on the left) and David Peterson (on the right). Source: https://www.youtube.com/watch?v=0D84dHOS0Yo (archived http://archive.is/gedXu)</figcaption></center>
</figure>


**Other Arbitraging promoters identified:**

* [Crypto Austin](https://www.youtube.com/user/austin19781978/videos) (archived [here](http://archive.fo/dIeMJ))
* [IL-Matt](https://www.youtube.com/user/1qimds/videos) (archived [here](http://archive.fo/Zybu0))
* [Matty Crytpo](https://www.youtube.com/channel/UC4mTheN92h05TkGkgVc1z7w) (archived [here](http://archive.fo/nTELv))
* [KineticEnergy](https://www.youtube.com/channel/UCJ6iHwvZp-KbcuRN2SAGV6w/videos) (archived [here](http://archive.is/Pjz7T))
* [CRYPTOEKEEPER](https://www.youtube.com/channel/UCKNB_g8jBz0Q-KE5KknUA5g/videos) (archived [here](http://archive.fo/y4cOM))
* [Crypto TiWi](https://www.youtube.com/user/tushervip/videos) (archived [here](http://archive.is/tyaGX))
* [PJ3 ICO Private I](https://www.youtube.com/channel/UCpMcAM5EHrhZEb0okKddelA/videos) (archived [here](http://archive.fo/Ax4Hs))
* [Bitsaway1](https://www.youtube.com/channel/UCkDzqga4zH_CcPhFQxqONNg/videos) (archived [here](http://archive.fo/u12zD))
* [shoemoney](https://www.youtube.com/user/shoemoney/videos) (archived [here](http://archive.fo/33j5e))
* [Whale Miner](https://www.youtube.com/channel/UCE5z86gfKCwzQ1RcFN22wAQ/videos) (archived [here](http://archive.fo/qfWn9))
* [REVOLUTION IN CRYPTO](https://www.youtube.com/channel/UCv53g2Cuc0ugvmpuuF9iSUQ/videos)(archived [here](http://archive.fo/HnJre))
* [Crypto Sensei](https://www.youtube.com/channel/UCSkgJ2pT157J9YnpmP6av-w/videos) (archived [here](http://archive.fo/X4jCk))

*****

## Dissecting David Peterson (CEO of Arbitraging)

<figure class="aligncenter">
  <img src="https://i.imgur.com/okOHmp9.png" />
  <center><figcaption>David Peterson (on the right) and Brock Pierce (on the left) at WorldCryptoCon 2019. Source: https://twitter.com/arbitragingco/status/1084388880646688768 (archived http://archive.is/iowXZ)</figcaption></center>
</figure>

David is considered a God in the Arbitraging community: he also makes videos about the platform and how to use it, he speaks directly to the investors in their Telegram groups and everybody gets crazy because of his creation.

But recently he made a [video](https://www.youtube.com/watch?v=exy80npYDnQ) (archived [here](http://archive.is/vphrY)) about his story and he also showed some personal images that I reverse searched on Google and Yandex. After a bit, I found a blog post from 2017 written by David in a fishing enthusiast website, called [In-Depth Outdoors](https://www.in-depthoutdoors.com/).

<figure class="aligncenter">
  <img src="https://i.imgur.com/S8fqjCb.png" />
  <center><figcaption>A blog post found with reverse images researches. Source: https://www.in-depthoutdoors.com/community/forums/topic/new-to-the-forum-after-tonight-i-think-ill-stick-around/</figcaption></center>
</figure>

His signature in this article was **Jeremy**, not David, and after more researches, I was able to find a company related to this man, called **Srills** that is selling products for plants and garden. Moreover, I found an [article](https://www.crookstontimes.com/news/20170425/minnesota-man-had-job-girlfriend-home---and-big-secret) of a daily newspaper of Crookston, a city of Minnesota **where the same Jeremy appears but this time his complete name was shown**:

<figure class="aligncenter">
  <img src="https://i.imgur.com/CgxBeF3.png" />
  <center><figcaption>Jeremy Rounsville, owner of Srills Products. Source: https://www.crookstontimes.com/news/20170425/minnesota-man-had-job-girlfriend-home---and-big-secret</figcaption></center>
</figure>

**Jeremy Rounsville**, the owner of Srill Products, is David Peterson CEO of Arbitraging and the following picture (and his hand-tattoo) found on Srill’s official Twitter profile confirmed it:

<figure class="aligncenter">
  <img src="https://i.imgur.com/zqtN7E0.png" />
  <center><figcaption>Jeremy Rounsville owner of Srills Products compared to David Peterson CEO of Arbitraging.co. Source: https://twitter.com/SrillsDotCom/status/612354922298908672 (archived http://archive.is/3Xaw9)</figcaption></center>
</figure>

*****

## Conclusion

> “If it looks like a duck, swims like a duck, and quacks like a duck, then it
> probably is a duck”

Investing in ICOs has high risks and people quite often try to get into the crypto game before it’s too late so they can cure their **FOMO** (Fear Of Missing Out) but there are some tips you can follow to avoid getting burned:

* **Educate your self** first and question everything
* More than 80% of ICOs [will probably fail](https://coinjournal.net/vitalik-buterin-90-icos-will-fail/) and go to zero. **Keep that in mind**.
* **Don’t invest** in an ICO simply because the company claims their coin will increase in value in the future
* **Unclear roadmap** of the project with extremely vague goals and **poor grammars** in the whitepaper are usually bad signs
* **Never trust YouTube promoters** that promise you back easy money without any risk, do your due diligence and research the subject of your potential investment
* **Follow well-respected figures in cryptocurrency** if you like the subject. There are many people on Twitter that have gained reputations for providing high-quality information to their followers, helping them to avoid scams
* **Avoid anonymous projects** that provide blurry information not confirmed by anyone: best way to scam people is by hiding your identity
* **Don’t trust services** without a proper [Identity Verification Service](https://en.wikipedia.org/wiki/Identity_verification_service) used by businesses to ensure that users or customers provide information that is associated with the identity of a real person

That’s it, I’m out.

#### If you liked this post, give me back some love.

<figure class="aligncenter">
  <img src="https://i.imgur.com/i3rvJLY.gif" />
  <center><figcaption></figcaption></center>
</figure>


