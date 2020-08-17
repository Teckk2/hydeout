---
layout: post
title: DIVA - Insecure Data Storage - Part 1
categories:
  - Mobile
---

<br>Next challange in the list is Insecure Data Storge.
<br>![3-1](https://teckk2.github.io/assets/images/DIVA/3-1.png)
<br>In this challenge we will try to understand how an application store a sensitive information inside the device in plain text or with weak encryption, which could later lead to data information leakage.
<br>![3-2](https://teckk2.github.io/assets/images/DIVA/3-2.png)
<br>In the password section I put (111222) or any random password you wish to save and click on save.
<br>Now for our next step we need to read some internal files and for that we would require root permission
<br>Now connect to android device with adb shell
<br>![3-3](https://teckk2.github.io/assets/images/DIVA/3-3.png)
<br>![3-4](https://teckk2.github.io/assets/images/DIVA/3-4.png)
<br>Check for connect devices
<br>![3-5](https://teckk2.github.io/assets/images/DIVA/3-5.png)
<br>As we can see our device is connect we are good to go
<br>![3-6](https://teckk2.github.io/assets/images/DIVA/3-6.png)
<br>We have the root shell now, we can read the internal file without restriction now
<br>![3-7](https://teckk2.github.io/assets/images/DIVA/3-7.png)
<br>As you can see there is a (shared_prefs) folder which means the application is storing these details using shared preferences
<br>If you analyze the source code you will get the clear understanding
<br>![3-8](https://teckk2.github.io/assets/images/DIVA/3-8.png)
<br>![3-9](https://teckk2.github.io/assets/images/DIVA/3-9.png)
<br>Now get back to adb shell
<br>![3-10](https://teckk2.github.io/assets/images/DIVA/3-10.png)
<br>As you cans see the credentials are being saved in plain text inside the device.

<p class="message">
  ~ tavşanı sever
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
