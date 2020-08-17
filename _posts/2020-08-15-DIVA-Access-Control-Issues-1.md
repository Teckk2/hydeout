---
layout: post
title: DIVA - Access Control Issues - Part 1
categories:
  - Mobile
---

<br>This challange is about bypassing access controls, let's find out how to solve this.
<br>![9-1](https://teckk2.github.io/assets/images/DIVA/9-1.png)
<br>![9-2](https://teckk2.github.io/assets/images/DIVA/9-2.png)
<br>By clicking the View API Credentials we can see the credentials.
<br>But the objective of this challenge is to access the API credentials without clicking the view button, there are couple of ways to do this, let’s try and find the most prominent way.
<br>To understand the cause of this vulnerability let’s read the (AndroidManifest.xml)
<br>![9-3](https://teckk2.github.io/assets/images/DIVA/9-3.png)
<br>If you remember we just unzipped the apk, that’s the reason the file is still in Android binary xml format, in able to read this file we need to decode the Apk properly using apktool
<br>![9-4](https://teckk2.github.io/assets/images/DIVA/9-4.png)
<br>![9-5](https://teckk2.github.io/assets/images/DIVA/9-5.png)
<br>To understand the issue you need to focus on this piece of code
<br>![9-6](https://teckk2.github.io/assets/images/DIVA/9-6.png)
<br>The intent-filter is generally used for protection mechanism, but if you use it with activity then it can be even used to export publicly. Which will allow any application from outside to use this activity and view the API credentials.
<br>Now close your application in the emulator or you physical device, wherever you are testing
<br>![9-7](https://teckk2.github.io/assets/images/DIVA/9-7.png)
<br>Now open ADB shell and write the following command anyone of the below, If you are outside the adb shell just type
<br>**{adb shell am start jakhar.aseem.diva/.APICredsActivity}**
<br>![9-8](https://teckk2.github.io/assets/images/DIVA/9-8.png)
<br>**{ adb shell am start -n jakhar.aseem.diva/.APICredsActivity -a jakhar.aseem.diva.action.VIEW_CREDS }**
<br>![9-9](https://teckk2.github.io/assets/images/DIVA/9-9.png)
<br>If you are inside adb shell you can just type this
<br>**{ am start jakhar.aseem.diva/.APICredsActivity }**
<br>![9-10](https://teckk2.github.io/assets/images/DIVA/9-10.png)
<br>The moment the command get executed you will see the API credential popup on the screen
<br>![9-11](https://teckk2.github.io/assets/images/DIVA/9-11.png)

<p class="message">
  ~ tavşanı sever
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
