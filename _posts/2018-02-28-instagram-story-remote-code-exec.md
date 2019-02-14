---	
layout: post
date: 2018-02-28 01:00
title:  "How an Instagram’s Story drives me to a Remote Code Execution."
mood: happy
category: 
- docs
---


<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*B6EHd2SADThdcK2AwxuFfg.jpeg" />
  <figcaption></figcaption>
</figure>

### DISCLAIMER

> All information shared are for educational purposes only. Use these at your own discretion and remember: **you are responsible for any damages caused**. Actually, think about how this hack was possibile, how it could have been happened and, if you’re a dev, make sure to build more secure systems than that.
>
> **The views expressed on this article are my own and do not necessarily reflect the view of other people.**

<!--more-->

*****

### INTRODUCTION

These days are very hot in the infosec community, especially here in Italy. There are only a few days left before the next political elections and two of the biggest political parties have been hacked, at different levels and in different ways ([1](https://www.agi.it/politica/hacker_movimento_5_stelle-3461812/news/2018-02-08/), [2](http://formiche.net/2018/02/hacker-rousseau-polizia-postale/), [3](https://www.ilfattoquotidiano.it/2018/02/06/hackerato-il-sito-del-pd-di-firenze-anonplus-ci-sono-dati-di-matteo-renzi-dem-roba-vecchia/4140764/)). The discussion about *ethical hacking* reached its peak when a student was reported for revealing a [huge vulnerability in Rousseau](http://milano.repubblica.it/cronaca/2018/02/06/news/polizia_postale_denunciato_trentenne_accesso_abusivo_piattaforma_rousseau_cinque_stelle-188124666/), a major web-platform of the “Movimento 5 Stelle”, currently the biggest italian political party.

I don’t want to bring more items to this discussion since enough things have already been said so I thought it was cool to bring my vision of *ethical hacking* with a critical vulnerability that I found by chance thanks to an interesting Instagram Story.

### Instagram Stories: a brief introduction

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*rMdiusg9CK0cct-8kzWpTg.gif" />
  <figcaption></figcaption>
</figure>

A simple but effective way to describe the idea behind the Instagram Stories is the following statement that I found on a random marketing website and translated in english for the readers:

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*yfCrYJvkq87ItCx5ZHlaYQ.png" />
  <figcaption></figcaption>
</figure>

After the appropriate corrections, this statement looks perfect for the story I‘m going to share with you:

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*XxQA4ZS9ZKAh097HLwgkow.png" />
  <figcaption></figcaption>
</figure>

*****

### CHAPTER 1: “not interesting..” <swipe> “still not interesting..” <swipe> “again not interest…oh sh&ast;t!”

As already said in the introduction, during a sleepless night a particular Instagram Story caught my attention:

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*Mzh-k2GxdQKACsI8Wu0dRw.png" />
  <figcaption></figcaption>
</figure>

At first glance it appears innocent: this person just posted a pic about his/her upcoming school trip. Nothing new, I guess almost everyone see those pictures on Instagram every single day.

But if you look closer it’s possibile seeing something more interesting:

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*-H1f3PACGmpxdu-aOU1Uzg.png" />
  <figcaption></figcaption>
</figure>

Yes, that’s a **password** (redacted for obvious reasons) and a web-address to a **login portal** (also redacted for the same reasons). At that time, I don’t know if it worth or not but I tried to reach that address and the following page appears:

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*7yIb84eYE7RHL0z5mS2lXQ.png" />
  <center><figcaption>Login Page. (ENG: “Attention. You’re entering a restricted area)</figcaption></center>
</figure>

I guessed I have all information needed, so I typed down the password found and it worked.

The following picture shows the successfully login:

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*fV68CUPmMXZIi1dZzx1TaA.png" />
  <center><figcaption>Successfully login. (ENG: “Play the video” and “Enter the site”)</figcaption></center>
</figure>

>“Ok cool, but I don’t think there is too much I can do here. I don’t want to start poking with the web-application searching for bugs etc…”

*****

### CHAPTER 2: keep exploits attempts away

I started looking around **without forcing** anything but acting like a normal user. This portal offers a summary of the upcoming trip of the person who posted the photo on Instagram.

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*uXINOTG6ZUFCQpR4Dew0FA.png" />
  <center><figcaption>School lessons timetable.</figcaption></center>
</figure>

It’s possibile to retrive useful information like lessons timetables, addresses of schools and hotels, name of involved teachers and cellphones numbers. I mean, there are some sensitive information but nothing very interesting here also because the student can only access to the information of his school trips, he can’t see information about other school trips. **Well, not really.**

I started looking at the URL in the browser while I was browsing in the website and I notice that all the pages I can browse are in the same sub-domain. A couple of examples (*the original folder’s names have been changed*):

* *subdomain.domain.it/site/21443/docs/12231/TimeTable.pdf*
* *subdomain.domain.it/presentation/31223/index.html*
* *etc..*

So I browse to the root directory of the *subdomain.domain.it* and this page appeared in front of me:

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*BMn_gyPBLJJTdz9S92jgfQ.png" />
  <center><figcaption>Second login page found</figcaption></center>
</figure>

Ok, the temptation here was very strong, but I had already decided to not try to exploit anything. **Sorry, no injection attempts here.**

What I did was a **“manually knock-knock approach”**: just a couple of common auth combinations also with the previous password found but nothing was working and it was sad. **Sorry, no bruteforce here.**

After a few knock-knock I decided to try to open the door without using any keys, and surprisingly it worked.

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*47wI_cfCT4GYxlRvZEJrNg.gif" />
  <center><figcaption></figcaption></center>
</figure>

>No username and no password was actually the credentials used. Welcome to 2018 guys.

*****

### CHAPTER 3: Welcome back administrator!

After succesfully login, the web-application shows the following dashboard:

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*aba_ri7FHBFiZkx7DRKP_g.png" />
  <center><figcaption>Administrator dashboard found</figcaption></center>
</figure>

From now on, I can arbitrary modify indiscriminately every single trips information, as the following image shows:

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*Mnlg7QDgvEdxBqitGWaIyA.png" />
  <center><figcaption></figcaption></center>
</figure>

But the best feature I found was the following one:

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*lNxLr2vHliAeQYuDRGKdnA.png" />
  <center><figcaption>File upload function</figcaption></center>
</figure>

Yes, **arbitrary file upload**. This function is used for attach .pdf files with trip’s information for the students.

But, what if I try to upload a “non-pdf” file? **Let’s start with a text file**:

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*RLAmi9N8UX5qDFPkVYSdGQ.png" />
  <center><figcaption>Arbitrary files upload: txt file</figcaption></center>
</figure>

It worked, so it seems that there is **no check on the file’s extension**. Let’s try with a tiny .php file as follow:

```php
<? php echo "test"; ?>
```
As a penetration tester find the ability to run arbitrary php code on a web-server is obviously considered pretty bad:

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*rEc45tJuPh42xoK_qJq7CQ.png" />
  <center><figcaption>Arbitrary files upload: txt file</figcaption></center>
</figure>

**But there you go..BINGO!** The web-server interpreted successfully my tiny php file and I’d got all I needed in order to try to execute arbitrary code on this machine.

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*NMTTZDHrUlo-GJPVdxu9gQ.gif" />
  <center><figcaption>RCE dance</figcaption></center>
</figure>

*****

### CHAPTER 4: RCE!

In order to demonstrate a RCE I uploaded a php agent with weevely3: the agent is small, hardly detectable by AV software, and the communication between the client and the agent is obfuscated within HTTP requests.

This is the obfuscated PHP agent uploaded:

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*9AJegaG0CeBW9wlkSez4UQ.png" />
  <center><figcaption>PHP agent create with weevely3</figcaption></center>
</figure>

I renamed it as **“new_settings.php”** and successfully uploaded it to the server:

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*6GcnnVDwlKYqJxo_PbkXAA.png" />
  <center><figcaption></figcaption></center>
</figure>

After that I connect to the agent as follow and voilà:

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*IzNxIpGi9Qgjei24z85kiw.png" />
  <center><figcaption>Successfully connected to the weevely php agent</figcaption></center>
</figure>

**Remote Code Execution successfully obtained!**

I guees i’m done with it, it’s time to inform the vendor about what I found. How will they react to this?

*****

### CHAPTER 5: Responsible disclosure

<figure class="aligncenter">
  <img src="https://cdn-images-1.medium.com/max/1440/1*6awAhI1U48LLfB5pokeqMA.gif" />
  <center><figcaption></figcaption></center>
</figure>

* 26 February 2018: first email has been sent to the vendor. Also write on their “Support Live Chat” on the website. No immediate answer received.
* 27 February 2018: second email has been sent to the vendor. Also a first email has been sent to the agency that have developed this website.
* 27 February 2018: first answer from the agency: they are in contact with their client in order to solve the problem.
* 28 February 2018: they fixed the login page. But still no answer from them.