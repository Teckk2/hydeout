---
layout: post
title: DIVA - Insecure Data Storage - Part 2
categories:
  - Mobile
---

<br>Let’s start our 3rd part of the challenge in insecure data storage
<br>Open the application and put the credential and click save
<br>![5-1](https://teckk2.github.io/assets/images/DIVA/5-1.png)
<br>Before we solve this let’s have a look at the source code first
<br>![5-2](https://teckk2.github.io/assets/images/DIVA/5-2.png)
<br>![5-3](https://teckk2.github.io/assets/images/DIVA/5-3.png)
<br>As you can see in the code, the application create a temporary file to save the credential inside the device, let’s have a look
<br>![5-4](https://teckk2.github.io/assets/images/DIVA/5-4.png)
<br>![5-5](https://teckk2.github.io/assets/images/DIVA/5-5.png)
<br>The tmp file store the credential in plain text inside the device.

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
