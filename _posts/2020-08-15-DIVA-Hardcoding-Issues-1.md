---
layout: post
title: DIVA - Hardcoding Issues
categories:
  - Mobile
---

<br>Now let’s come to our next vulnerability which is Hardcoding Issues
<br>![2-1](https://teckk2.github.io/assets/images/DIVA/2-1.png)
<br>The one common mistake which many developers do while either making the web application or mobile application, they unintentionally forget to remove the hardcoded password or keys, which help an attacker to access sensitive information.
<br>To solve this challenge we need to follow the same steps which we did in the last challenge
<br>![2-2](https://teckk2.github.io/assets/images/DIVA/2-2.png)
<br>We need to use jad again to see the clear text of the file 
<br>![2-3](https://teckk2.github.io/assets/images/DIVA/2-3.png)
<br>_**KEY=**_ "vendorsecretkey"
<br>As you can see inside the code we can see the key, let’s try it inside application
<br>https://teckk2.github.io/assets/images/DIVA/2-4.png
<br>
<br>***Mükemmel*** As you can see the key worked perfectly and the access has been granted to us.

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
