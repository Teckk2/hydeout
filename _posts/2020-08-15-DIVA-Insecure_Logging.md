---
layout: post
title: DIVA - Insecure Logging
categories:
  - Mobile
---

<br>The first challange in DIVA is Insecure Logging
<br>![1-1](https://teckk2.github.io/assets/images/DIVA/1-1.png)
<br>![1-2](https://teckk2.github.io/assets/images/DIVA/1-2.png)
<br>Now to analyze our logs we will open logcat on the android studio
<br>[1-3](https://teckk2.github.io/assets/images/DIVA/1-3.png)
<br>If we open this we can see the logs the application is feeding with its stack trace when it generates any errors.
<br>![1-4](https://teckk2.github.io/assets/images/DIVA/1-4.png)
<br>Let’s feed the application with any random number to create an error
<br>![1-5](https://teckk2.github.io/assets/images/DIVA/1-5.png)
<br>And click on checkout
<br>![1-6](https://teckk2.github.io/assets/images/DIVA/1-6.png)
<br>As you can see the credit card number which we feed in the application is visible in logcat which is considered as an **Insecure Logging** vulnerability.
<br>Let's decomplie/unpack the APK to analyz the code which cause this vulnerbality in the application.
<br>Unzip the apk file
<br>![1-7](https://teckk2.github.io/assets/images/DIVA/1-7.png)
<br>Classes.dex this is what we need
<br>![1-8](https://teckk2.github.io/assets/images/DIVA/1-8.png)
<br>![1-9](https://teckk2.github.io/assets/images/DIVA/1-9.png)
<br>![1-10](https://teckk2.github.io/assets/images/DIVA/1-10.png)
<br>Inside **./jakhar/aseem/diva** we can find the file LogActivity.class which have vulnerable code which we are looking for
<br>![1-11](https://teckk2.github.io/assets/images/DIVA/1-11.png)
<br>Again we need to breakdown the file into normal readable text but this time we will use a different toll (jad)
<br>I guess in new kali 2020 they removed the jad from the repo
<br>You can download it from gitlab-[jad](https://gitlab.com/kalilinux/packages/jad)
<br>![1-12](https://teckk2.github.io/assets/images/DIVA/1-12.png)
<br>![1-13](https://teckk2.github.io/assets/images/DIVA/1-13.png)
<br>![1-14](https://teckk2.github.io/assets/images/DIVA/1-14.png)
<br>As you can see this is the piece of code which logs the data of credit card no. from the application in Logcat. 
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Log.e("diva-log", (new StringBuilder()).append("Error while processing transaction with credit card: ").append(edittext.getText().toString()).toString());
<br>Toast.makeText(this, "An error occured. Please try again later", 0).show();
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
