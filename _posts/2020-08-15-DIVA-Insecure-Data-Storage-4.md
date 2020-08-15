---
layout: post
title: DIVA - Insecure Data Storage - Part 4
categories:
  - Mobile
---

<br>Now let’s go onto our last challenge of insecure data storage
<br>![6-1](https://teckk2.github.io/assets/images/DIVA/6-1.png)
<br>When you are trying to save the credential you may face this issue, that file error occurred, this is because the application don’t have permission to create file in sdcard, so we can just open app info
<br>![6-2](https://teckk2.github.io/assets/images/DIVA/6-2.png)
<br>Click on permissions
<br>![6-3](https://teckk2.github.io/assets/images/DIVA/6-3.png)
<br>And enable the storage permission
<br>Come back to the app, and you could be able to save the credential now.
<br>Before we solve just quickly have a look at the source code first
<br>![6-4](https://teckk2.github.io/assets/images/DIVA/6-4.png)
<br>When you analyze the code, you will see the application is storing the credential inside sdcard with a hidden file of .uinfo.txt
<br>![6-5](https://teckk2.github.io/assets/images/DIVA/6-5.png)
<br>Now let’s back to our adb shell
<br>![6-6](https://teckk2.github.io/assets/images/DIVA/6-6.png)
<br>In /sdcard folder we can see .uinfo.txt as mention in the sourcecode
<br>![6-7](https://teckk2.github.io/assets/images/DIVA/6-7.png)
<br>And here is our credential in clear text


<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
