---
layout: post
title: DIVA - Environment setup
categories:
  - Mobile
---

<br>While setting up the environmenty and solving DIVA, I did few reddendent steps and followed a long way becasue my objective was not just to solve the app and show you, but to learn more and more methods and the mistaked I did while solving this. So if you don't like any step or part, feel free to skip it.
<br>Let's start by downloading [DIVA APK](http://www.payatu.com/wp-content/uploads/2016/01/diva-beta.tar.gz) from the official site of [Payatu](https://www.payatu.com/).
<br>Then we need to download [Android Studio](https://developer.android.com/studio) to emulate our Android phone.
<br>![0-1](https://teckk2.github.io/assets/images/DIVA/0-1.png)
<br>Click on profile or debug APK
<br>![0-2](https://teckk2.github.io/assets/images/DIVA/0-2.png)
<br>When you open your APK make sure it install SDK or if doesn’t do itself, just close the project and reopen again, or find a manual way to do it
<br>![0-3](https://teckk2.github.io/assets/images/DIVA/0-3.png)
<br>Now click on No Device and click on Open AVD Manager
<br>![0-4](https://teckk2.github.io/assets/images/DIVA/0-4.png)
<br>Click on Create Virtual Device
<br>![0-5](https://teckk2.github.io/assets/images/DIVA/0-5.png)
<br>Pick the device you want as a virtual device but make sure to select a device without playstore because if you select the device with playstore it won’t allow you to access as root with adb-shell
<br>![0-6](https://teckk2.github.io/assets/images/DIVA/0-6.png)
<br>Click the image which you want to install, in our case we will go with Nougat for stability
<br>Once the OS is downloaded click the image and proceed to next step
<br>![0-7](https://teckk2.github.io/assets/images/DIVA/0-7.png)
<br>![0-8](https://teckk2.github.io/assets/images/DIVA/0-8.png)
<br>Change the name of the Device as per your wish and proceed to finish
<br>![0-9](https://teckk2.github.io/assets/images/DIVA/0-9.png)
<br>Now click launch
<br>Once we setup the emulator we can see the device showing in our project to be launched
<br>![0-10](https://teckk2.github.io/assets/images/DIVA/0-10.png)
<br>![0-11](https://teckk2.github.io/assets/images/DIVA/0-11.png)
<br>And we got the emulator up and running
<br>If it couldn’t see the DIVA application then you must have missed some steps, try doing it again.
<br>![0-12](https://teckk2.github.io/assets/images/DIVA/0-12.png)
<br>![0-13](https://teckk2.github.io/assets/images/DIVA/0-13.png)
<br>Now download and install the following tools which we could require for latter debugging
<br>![0-14](https://teckk2.github.io/assets/images/DIVA/0-14.png)

<br>• **apt-get install dex2jar**
<br>• **apt-get install jd-gui**
<br>• **apt-get install apktool**
<br>• **apt-get install abd**
<br>• **apt-get install sqlite3**


<br> We are done with all the setup, time to do some action now.
<div class="background-wrap">
	<video id="video-bg-elem" preload="auto" autoplay="true" loop="loop" muted="muted">
		<Source src="https://media.giphy.com/media/XgSuqXMnL9x9ZOKnTh/giphy.mp4">
	</video>
</div>

<p class="message">
  ~ tavşanı sever
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
