---
layout: post
title: DIVA - Insecure Data Storage - Part 2
categories:
  - Mobile
---

<br>Next few challenges are all about insecure data storage, so let’s go
<br>![4-1](https://teckk2.github.io/assets/images/DIVA/4-1.png)
<br>![4-2](https://teckk2.github.io/assets/images/DIVA/4-2.png)
<br>I put the credential as [Teck_k2:Teck_k2] and save
<br>Before we proceed further, we will check the code which allow this insecure data storage vulnerability to happen.
<br>Let’ back again to our kali
<br>![4-3](https://teckk2.github.io/assets/images/DIVA/4-3.png)
<br>Extract the file content, and analyze
<br>![4-4](https://teckk2.github.io/assets/images/DIVA/4-4.png)
<br>As you can see this piece of code inserting the credential into sql database inside the device, Now let’s come back to our adb shell and extract the database file
<br>![4-5](https://teckk2.github.io/assets/images/DIVA/4-5.png)
<br>As you can see the databases folder is available, let’s go inside the folder and see all the available files
<br>![4-6](https://teckk2.github.io/assets/images/DIVA/4-6.png)
<br>Generally we need to analyze all file one by one, but as this is a specific challenge based scenario, we won’t waste much time in analyzing all the files
<br>For this challenge specifically we just need (ids2), we will extract this file in our local machine, for that we need to run adb as root first and then extract or it will show you permission error or file not found.
<br>![4-7](https://teckk2.github.io/assets/images/DIVA/4-7.png)
<br>![4-8](https://teckk2.github.io/assets/images/DIVA/4-8.png)
<br>Move the file in your kali and open it with slqlite3
<br>![4-9](https://teckk2.github.io/assets/images/DIVA/4-9.png)
<br>As you can see the clear text credentials are saved inside the sql database locally inside the device.


<p class="message">
  ~ tavşanı sever
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
