---
layout: post
title: DIVA - Input Validation - Part 3
categories:
  - Mobile
---

<br>We reached to our final challenge in this the objective is to do DOS the application and crash it
<br>![13-1](https://teckk2.github.io/assets/images/DIVA/13-1.png)
<br>As the hint mention that this is a classic example of memory corruption or stack based buffer overflow
<br>![13-2](https://teckk2.github.io/assets/images/DIVA/13-2.png)
<br>As you can see there is strcpy function available in the library of the application, so let’s try with something simple to understand where we are
<br>![13-3](https://teckk2.github.io/assets/images/DIVA/13-3.png)
<br>Generate a string of A’s and feed it inside the application to see the response in Logcat
<br>**AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA**
<br>![13-4](https://teckk2.github.io/assets/images/DIVA/13-4.png)
<br>Now push the red button
<br>![13-5](https://teckk2.github.io/assets/images/DIVA/13-5.png)
<br>And you will notice the application crashed successfully
<br>The real fun start now, to exploit a binary in Android, which kept me and **KNX** busy for almost a month (Binary from Hell).

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
