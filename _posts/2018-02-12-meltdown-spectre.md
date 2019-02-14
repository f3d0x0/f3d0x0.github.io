---	
layout: post
date: 2017-06-29 01:00
title:  "Meltdown and Spectre — When the problems are really at the lowest level"
mood: happy
category: 
- docs
---


<figure class="aligncenter">
  <img src="https://media.licdn.com/dms/image/C4E12AQHOhGbJsRgg9Q/article-inline_image-shrink_1500_2232/0?e=1555545600&v=beta&t=Y73KSg-rqYXUggyzxYgOvqbFuqZuDnTKHsKJspJgfEQ" />
  <figcaption></figcaption>
</figure>


From the beginning of 2018 two vulnerabilities that undermine the security of all modern microprocessors (Intel first, but not only) have been discovered, thus putting at risk the vast majority of the ICT worldwide.

<!--more-->

These are the vulnerabilities called **“Meltdown”** and **“Spectre”**. Actually two different ways to exploit the same flaw, with different effects. Their potential is to completely disclose the contents of system memory, and they are enabled by the abuse of the optimization technique adopted by modern CPUs, called **speculative execution**, used to improve computational performance.

>“Speculative execution is an optimization technique where a computer system performs some task that may not be needed. Work is done before it is known whether it is actually needed, so as to prevent a delay that would have to be incurred by doing the work after it is known that it is needed. If it turns out the work was not needed after all, most changes made by the work are reverted and the results are ignored.” (source: Wikipedia)

Quoting the Wikipedia definition above, *“If it turns out the work was not needed after all, most changes made by the work are reverted and the results are ignored.”*

Remember this sentence, we’re going back on it in a while.

<figure class="aligncenter">
  <img src="https://media.licdn.com/dms/image/C4E12AQFlK3oHx_MF6g/article-inline_image-shrink_1000_1488/0?e=1555545600&v=beta&t=W1qfKwDUOPrJ6HF_FhXPB1YFvUexHLqj2H7KzIKPRZY" />
  <figcaption></figcaption>
</figure>

This flaw had a very broad and immediate media resonance, in fact the implication is the possibility of obtaining the entire content of the memory, by executing code on a vulnerable machine. Not only that: this ability crosses the boundaries between physical and virtual memory and, in a specific variant, this flaw allows even to read the memory content of the physical host machine from the virtual guest machine. Furthermore, the execution of malicious code does not necessarily require the execution of a malicious software (i.e. an “exe file”). The success has also been demonstrated by acting within a browser. **In short, just visit a malicious website, without downloading attachments, puts at risk the entire memory content of the machine (including private keys, passwords, etc.)**

Different variants of this attack have different impact on the current processors available in the market. In fact almost all modern microprocessors are affected by these vulnerabilities, if attacked with these approaches (why Raspberry PI isn’t affected?). The reason lies in the architectural choices made over the last 10–15 years aimed at improving performance. According to different approaches and driven by increasingly sophisticated heuristics, today a processor can execute in parallel many sets of instructions provided that they are independent of each other, even in a “predictive” way, i.e. “betting” that their execution will be useful in a short time. Of course it is assumed that, if the execution was not useful, **or even worse it should not have been authorized**, it would have been possible to restore the previous architectural state without leaving any trace. **Well, this assumption has been proved to be false.** ¯\_(ツ)_/¯

<figure class="aligncenter">
  <img src="https://media.licdn.com/dms/image/C4E12AQHuG71qyiGLSw/article-inline_image-shrink_1500_2232/0?e=1555545600&v=beta&t=m8fuImdg-Z5-mNEvBQz2IXh4kuxCVcSE3sAOELmDuGE" />
  <figcaption></figcaption>
</figure>

Usually, a researcher finds a bug and gives vendors a few months to fix the problem before to disclose it to the public. But as those bugs affect more companies and more products, this path becomes more complex. More people need to be told and kept in confidence as more software needs to be quietly updated and pushed out.

>"With Meltdown and Spectre, that multi-party coordination broke down and the secret spilled out before anyone was ready."

Vendors were aware about the vulnerabilities since mid-2017, and patching was ongoing, in fact most of the OS manufacturers had prepared patches for the beginning of 2018 (some patches were already released at the end of 2017, without stating the exact purpose). However, publish the patch code for open-source systems such as Linux, even trying to avoid excessive rumors, has led to an early disclosure of the whole issue.

As already mentioned, all modern processors make “bets” on the instructions that will be executed after the current one. In the following image (originally taken from the [Meltdown paper](https://meltdownattack.com/meltdown.pdf)) some comments were added in order to make it clearer for the reader.

<figure class="aligncenter">
  <img src="https://media.licdn.com/dms/image/C4E12AQEp4UxV85AEAQ/article-inline_image-shrink_1500_2232/0?e=1555545600&v=beta&t=8bAIZlovKt-nwCPOQlw_UT2cyJGIhjk834MSm3JmGbs" />
  <figcaption></figcaption>
</figure>

In practice, as said all modern processors make “bets” on the instructions that will be executed after the current one, and that’s because the current instruction in the logical flow may be waiting for internal checks on permissions, or for data to be recovered from slower access memory. To avoid slowing down the execution, if the output of the following instructions does not depend on the processing of the locked one, the processor, having the resources, starts to execute them. Naturally, if the anticipated execution did not have to take place, the effects are canceled and the correct flow proceeds, without other consumption of resources except for a negligible waste of energy.

The complete “logical” isolation is not accompanied by an equally rigid independence from measurable physical parameters (e.g. access times to the information involved in the processing)

 Like many times has happened in modern cryptoanalysis, the evaluation of physical quantities associated with the elaboration of a given data permits to guess the data itself.

 >Today the concepts of “CPU” and “memory” are extremely blurred.

 In fact:

 * A CPU is equipped with several “cores”, each is internally very complex and is able to break down each instruction in “micro-operations”
* Such micro-transactions (at least most of them) are independent of each other and can be anticipated while waiting for others to be completed
* To achieve this, a complex planning architecture orchestrates everything, and the scheduler ensures that the final execution is properly ordered
* The memory is actually realized through hardware of different speed, in relation to the “proximity” to the processor (various levels of cache, to temporarily store the most used data and access it faster)
* Moreover, physical memory is mapped into virtual memory, in which different spaces are characterized by different access permissions
* Applications run in “user-mode” can’t access *in theory* the memory used by other applications or by the Operating System
* The Operating System, on the other hand, can access the memory of all the applications

**The combination of all these factors paves the way for a brand new series of attacks.**

Meltdown is the most serious of these attacks strategies, in terms of potential effects, and it can be exploited to read the contents of the private memory assigned to the kernel starting from programs with normal user access privileges.

Despite this, the vulnerability is quite simple to explain and trivial to exploit. The following code shows how the exploit looks like, in steps:

<figure class="aligncenter">
  <img src="https://media.licdn.com/dms/image/C4E12AQEPXK7DBt235A/article-inline_image-shrink_1500_2232/0?e=1555545600&v=beta&t=jef-JyNupnj4wpbd33G4fdHeZa0pBiJDG-o_MUFL2Xk" />
  <figcaption></figcaption>
</figure>

Compared to Meltdown, Spectre attacks require more specific strategies and knowledge of the target application memory space, however they are simpler to implement and more difficult to contrast. The purpose in fact is not to illegally read the kernel memory, but the memory of other applications.

A possible starting point is the **incorrect prediction** (which can also be specifically triggered) of the result of “if” conditions. In details:

* Suppose that a malicious application can legitimately access an array of a certain size
* Suppose that “at distance x” from the beginning of the array, out of the reachable space, there is a secret value K to obtain
* Given certain conditions (K cached, length of the *array1* and contents of the *array2* not cached), it’s possible to obtain the secret value K

The legitimate question, compared to the alert level to be associated with this attack strategy, has an immediate response: some variants of this attack can be implemented even in Javascript!

<figure class="aligncenter">
  <img src="https://media.licdn.com/dms/image/C4E12AQGl4k-zOmoy8Q/article-inline_image-shrink_1000_1488/0?e=1555545600&v=beta&t=iPc7SyyEPzjK7KATrAtC7Wy65KkMlk9T0F1eQ-egM3M" />
  <figcaption></figcaption>
</figure>

In fact, every site visited through an outdated browser potentially can achieve full access to portions of memory controlled by the browser itself, and this enables the ability to obtain data between browsing tabs simultaneously open. But this is only the a “best case”.

With the help of the following pseudocode, we describe a simple scenario where a Spectre variant could obtain illegal access to the memory:

<figure class="aligncenter">
  <img src="https://media.licdn.com/dms/image/C4E12AQFhr5rz8bpSRQ/article-inline_image-shrink_1500_2232/0?e=1555545600&v=beta&t=FIj5It33K1WcKWw-RNel3NZq3Pd6kj1RfbVCCAFVoMA" />
  <figcaption></figcaption>
</figure>

The above pseudocode could be simply rewritten in Javascript in the following way:

```javascript
if (index < simpleByteArray.length) {
    index = simpleByteArray[index | 0];
    index = (((index * TABLE1_STRIDE) | 0) & (TABLE1_BYTES-1)) | 0
    localJunk ^= probeTable[index | 0] | 0;
}

```

Some notes even if the situation continuously evolves:

* **At the processor level**: the Meltdown vulnerability applies to all outstanding Intel architectures (both Windows and Apple). There are also signs of applicability to ARM. However, practically no architecture is immune to the Spectre variants.
* **At the Operating System level**: the problems afflict the world of Windows, iOS and OSX, Android, as well as all the variants of the Unix / Linux. All vendors issued patches, but the effectiveness is related to the processor patching level. **Microsoft** has already released a patch via Windows Update. **Android** operating system has also received a security update which fixes the vulnerability and is incorporated in the January Security Patch. Due to the [Android fragmentation problem](http://www.businessinsider.com/android-fragmentation-is-worsening-2017-11?IR=T) not all Android manufacturers are quick in releasing these updates and your device may still be at [risk](https://source.android.com/security/bulletin/2018-01-01). Apple has responded to the leaks with [software updates](https://support.apple.com/en-us/HT208394) and now both iOS and macOS are protected against Meltdown, with a fix for Spectre coming soon.
* **At browser level**: all “known” browsers are now updated.
* **Gaming consoles**: no specific fixes for the current gaming consoles have been released.
* **Network devices**: e.g. Cisco is still releasing patches for their products (more info here). In fact Cisco is a peculiar vendor due to the fact it is possible to run custom code on his products. Devices without this feature *could* not be at risk.
* **Other devices**: ?

Unfortunately, in this case the vulnerabilities are strictly related to the strategies for executing machine instructions at hardware level, so they are transparent compared to the level of visibility offered by the software.

This has significant implications because the only efficient strategy should be the complete redesign of the CPUs, or at least a firmware patching but with the following considerations:

* the firmware update has potentially significant performance impacts on non-recent CPUs
* total replacement of CPUs is not feasible (also the most severe CERT doesn’t suggest it as a possible workaround)
* in any case it is necessary to update the software components (OS, browsers, middleware..) of the devices, too, with the latest patches/fixes


<figure class="aligncenter">
  <img src="https://media.licdn.com/dms/image/C4E12AQEXvHa_YtbTfg/article-inline_image-shrink_1500_2232/0?e=1555545600&v=beta&t=DuuV8XZK9daT28jzIu6aAmRtHjdvexSWF3TUgL8JGKY" />
  <figcaption></figcaption>
</figure>

### How to mitigate them? (for techie guys)

To resolve the Meltdown vulnerability (loss of isolation between the memory accessible in user-mode and in kernel-mode) the **kernel page-table isolation** (KPTI) functionality was introduced.

<figure class="aligncenter">
  <img src="https://media.licdn.com/dms/image/C4E12AQFOoh2eDw3PzQ/article-inline_image-shrink_1500_2232/0?e=1555545600&v=beta&t=e83jgTze1-bjIuJSRorYLMtaQmU2uGAIQYIDjNmc0qk" />
  <figcaption></figcaption>
</figure>

This mitigation gives each application two sets of pages tables rather than one and switches between them on every kernel-to-user and user-to-kernel transition in order to prevent the data disclosure during speculative execution.

Instead, to solve Spectre’s **Bounds Check Bypass** vulnerability, which takes advantage of speculative access to portions of data arrays beyond legitimate boundaries, there is not really a single strategy. There is a special instruction (**LFENCE**) that can be inserted into the code to stop speculative execution but the performance impact of its use risks being high.

To solve the Spectre’s **Brench Target Injection** vulnerability there is a strategy compilation developed by Google called **Redpoline** (Return Trampoline). This mitigation use a special cache that can be easily canceled in case of “wrong speculation”, thus blocking the measurable physical effects of prediction error. More info here.

### References

[1] https://meltdownattack.com/

[2] https://spectreattack.com/spectre.pdf

[3] https://meltdownattack.com/meltdown.pdf

[4] https://googleprojectzero.blogspot.it/2018/01/reading-privileged-memory-with-side.html

[5] https://medium.com/@mattklein123/meltdown-spectre-explained-6bc8634cc0c2

[6] https://github.com/IAIK/meltdown

[7] http://datasciencetidings.com/meltdown-and-spectre-exploits-and-mitigation-strategies/

[8] https://steemit.com/steemstem/@rebelheart/the-processor-bug-everything-you-need-to-know-about-the-massive-meltdown-and-spectre-leaks-and-how-it-affects-your-computer

[9] http://www.businessinsider.com/android-fragmentation-is-worsening-2017-11?IR=T

[10] https://source.android.com/security/bulletin/2018-01-01