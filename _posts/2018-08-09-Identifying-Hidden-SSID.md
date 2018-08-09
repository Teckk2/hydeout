---
layout: post
title: Identifying Hidden SSID
categories:
  - Wifi Pentesting
---

<br>Hidding your **SSID** will come in best practice but it's not a full prove security measure, an attacker can easily send a de-auth packet and Identify the hidden SSID of the AP.
<br>
<br>Setting up the environment
<br>![1](https://teckk2.github.io/assets/images/Wifi/4.PNG)
<br>Now open airodum and analyse
<br>![2](https://teckk2.github.io/assets/images/Wifi/5.PNG)
<br>As you can see the SSID is not showing any name
<br>let's anylyze that perticular AP
<br>![3](https://teckk2.github.io/assets/images/Wifi/6.PNG)
<br>![4](https://teckk2.github.io/assets/images/Wifi/7.PNG)
<br>Now keep analysing the AP untill any new client join it, or if there is any clinet already you can just send de-auth packet and when the clinet will try to re-join the AP, we will get the SSID.
<br>![5](https://teckk2.github.io/assets/images/Wifi/8.PNG)


<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
