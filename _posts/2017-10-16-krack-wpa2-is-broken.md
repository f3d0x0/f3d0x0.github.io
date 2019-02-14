---	
layout: post
date: 2017-10-16 01:00
title:  "KRACK: WPA2 is broken, what now?"
mood: happy
category: 
- docs
---


<figure class="aligncenter">
  <img src="https://media.licdn.com/media/gcrc/dms/image/C4E12AQH6R4xZ2cwVlw/article-cover_image-shrink_600_2000/0?e=1555545600&v=beta&t=8uQQQ-YSDQBZK9pCaCwovG5iAumF_FZsiYQcdjiYaUk" />
  <figcaption></figcaption>
</figure>


It's monday morning, i'm on a train heading to a conference and my earphones are broken. So instead of listening to music I opened my Twitter's feed and spot an interesting news retwetted by Troy Hunt:


<figure class="aligncenter">
  <img src="https://media.licdn.com/dms/image/C4E12AQH-nbeIycwHYA/article-inline_image-shrink_1500_2232/0?e=1555545600&v=beta&t=MffmGfm3GnvJStJTmcUglVtJr6RxlaxGFlP1LgEBzeg" />
  <figcaption></figcaption>
</figure>

<!--more-->

I read a lot of documents, articles and papers about WiFi security and spend a lot of time with tools that implements WiFi attacks. Why? Because simply I love hacking and in the last years I do some WiFi assessments and penetration tests as well for my company.


**So this news seems very juicy.**

This article was just an "introduction" of this new attack because at the time I was reading it, the public disclosure was ehm.. not public yet.

<figure class="aligncenter">
  <img src="https://media.licdn.com/dms/image/C4E12AQGbi8Tk_vHlHg/article-inline_image-shrink_1500_2232/0?e=1555545600&v=beta&t=jz6Q3cCyvzftfllqqxSl9QLkGxJpuA8Vv0RHJ_1ibtU" />
  <figcaption></figcaption>
</figure>


After lunch the public disclosure was online: the authors setup a [website](https://www.krackattacks.com/) and a GitHub where a PoC will be push: yes, will be, because the same authors decide not to publish a working exploit, but just a video (see below) with all the technical details written in the paper. BTW a PoC exploit will be release soon!


<iframe width="560" height="315" src="https://www.youtube.com/embed/Oh4WURZoR98" frameborder="0" allowfullscreen></iframe>

In the meanwhile a lot of sensational titles start to appear online:

<figure class="aligncenter">
  <img src="https://media.licdn.com/dms/image/C4E12AQEFd0krv_h4lg/article-inline_image-shrink_1500_2232/0?e=1555545600&v=beta&t=u4KEbQEe-Tw_Zhvms5115E6T00cs138HLym3Fghezsk" />
  <figcaption></figcaption>
</figure>

So I decide to do my homework (*and this is what every journalist did, right?*) and start analyzing the published paper trying to better understand what this attack really means to us. I don't give you too much technical details ([read](https://papers.mathyvanhoef.com/ccs2017.pdf) the paper in this case) but just my point of view about this awesome work (kudos to Mathy Vanhoef and Frank Piessens, the authors).

So, what's the core of this vulnerability? **The WiFi 4-way handshake.**


<figure class="aligncenter">
  <img src="https://media.licdn.com/dms/image/C4E12AQFWj0RshUDdXA/article-inline_image-shrink_1500_2232/0?e=1555545600&v=beta&t=KectC8CkOaSE77GWzTzY4itxS0zhkvsRf3NY_-G22-M" />
  <figcaption></figcaption>
</figure>



All the protected WiFi networks use the 4-way handshake to generate a fresh session key and the authors discovered that they were able to abuse this paradigm to triks a victim into reinstalling an **already-in-use key**.

**Mmm ok but, why this is bad?**

Short story: when a device reinstalling an already-in-use key, the associated parameters such as the incremental transmit packet number (**nonce**) and receive packet number (**replay counter**) are reset to their initial value. Not every WiFi implementation response the same way, **the impact depends on the handshake attacked and on the data-confidentiality protocol in use** (e.g. AES-CCMP, WPA-TKIP, GCMP).

So what is the impact?

It depends on the data-confidentiality protocol, as already said:

* **AES-CCMP**: in this case an attacker can reply and decrypt (but not forge) arbitrary packets. It also possibile to hijack TCP streams and inject malicious data into them.
* **WPA-TKIP and GCMP**: well, here the impact is catastrophic: packets can be replayed, decrypted and forged. ¯\_(ツ)_/¯ 

This worse scenario happen with 2.4 and 2.5 versions of **wpa_supplicant**, a WiFi client commonly used on Linux. This client will install an all-zero encryption key instead of reinstalling the real key. Also Android uses a modified version of **wpa_supplicant** and in particular Android 6.0 and Android 2.0 are susceptible to this attack: **these versions cover the 31.2% of all Android devices on the market!**

<figure class="aligncenter">
  <img src="https://media.licdn.com/dms/image/C4E12AQHUskfrTYR38w/article-inline_image-shrink_1000_1488/0?e=1555545600&v=beta&t=XKItZPVomAQvZVgEh7s90nk4yox41ID3spkAv5WL0Y0" />
  <figcaption></figcaption>
</figure>

What can I do for mitigate this issue?

* Patch, patch and patch. Don't ask, just patch your damn software. There is a public list of all the vendors statements [here](https://www.bleepingcomputer.com/news/security/list-of-firmware-and-driver-updates-for-krack-wpa2-vulnerability/). Check it!
* If a device (e.g. a router) can't be patched for some reasons, a patched client that connects to him mitigate the issue. **So don't be paranoid**, you're not exposed and don't throw anything out of the windows, it could be fixed! :)
* Linux users: a patch is already available [here](https://w1.fi/security/2017-1/)
* Windows and Mac users: **you are not vulnerable this time** (or better: the attack doesn't realistically work against you). And you know why? Because your OS's don't accept retransmissions of message 3 (see the paper for more details) and **this violated the 802.11 standard**. That's hilarious!

That's all for today. Just a little reminder for all the manufacturers:

<figure class="aligncenter">
  <img src="https://media.licdn.com/dms/image/C4E12AQHRbY-tWEqJDA/article-inline_image-shrink_1000_1488/0?e=1555545600&v=beta&t=U40BrhYtn5o1HXYSwH8nfciIb2PC7XwX3SrobLL6SMQ" />
  <figcaption></figcaption>
</figure>