---
layout: post
title: DIVA - Hardcoding Issues - Part 2
categories:
  - Mobile
---

<br>This challenge is the second part of Hardcoding issues, where the objective is to find sensitive information which is the vendor code left by developer inside the application source code.
<br>![12-1](https://teckk2.github.io/assets/images/DIVA/12-1.png)
<br>Let’s have a look inside source code
<br>![12-2](https://teckk2.github.io/assets/images/DIVA/12-2.png)
<br>![12-3](https://teckk2.github.io/assets/images/DIVA/12-3.png)
<br>After analyzing the code above, we can understand that the activity is creating another class with the name of DivaJni, let’s have a look at that.
<br>![12-4](https://teckk2.github.io/assets/images/DIVA/12-4.png)
<br>After analyzing the code above we could understand that there is a native library with the same name divajni, if you unzip the APK you will see the lib folder, which contains all the libraries inside it, let’s have a look
<br>![12-5](https://teckk2.github.io/assets/images/DIVA/12-5.png)
<br>Let’s open any of the library and analyze it
<br>![12-6](https://teckk2.github.io/assets/images/DIVA/12-6.png)
<br>After trying couple of strings, I finally found the correct string which can give us access **[olsdfgad;lh]**
<br>![12-7](https://teckk2.github.io/assets/images/DIVA/12-7.png)
<br>Finally we found the correct key, see you in the last challenge.

<p class="message">
  ~ tavşanı sever
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
