---
layout: post
title: Understand and Cracking WPA/WPA2(Enterprise)
categories:
  - Wifi Pentesting
---

<br>WPA2-Enterprise has been around since 2004 and is still considered the gold standard for wireless network security, delivering over-the-air encryption and a high level of security. But don’t think that it’s gotten any easier to deploy in that time. Regardless of whether you are deploying it for the first time or a seasoned expert, there are always unique challenges ready to give you a headache.
<br>First we need to setup our environment for which we will use Hostapd tool, which will create a fake radius server and also host the rouge AP.

<p>First Download some dependencies before we download our tool hostapd</p>
<br>![1](https://teckk2.github.io/assets/images/Wifi/34.PNG)
<br>![2](https://teckk2.github.io/assets/images/Wifi/20.PNG)
<br>![3](https://teckk2.github.io/assets/images/Wifi/21.PNG)
<br>Now open the hostapd-wpe.conf file
<br>![4](https://teckk2.github.io/assets/images/Wifi/22.PNG)
<br>And change the SSID if you want
<br>![5](https://teckk2.github.io/assets/images/Wifi/23.PNG)
<br>![6](https://teckk2.github.io/assets/images/Wifi/24.PNG)
<br>Now kill all the running process like wpa_supplicant and dhclient which can create problem for us while running virtual AP, and make sure your wifi card is connected to your kali machine and up and running.
<br>![7](https://teckk2.github.io/assets/images/Wifi/25.PNG)
<p>Now the Scenario is we named our AP same as our target AP which is Teck_k2-AP Now from another laptop or another Wifi card, we can put that in monitor mode and check the target AP BSSID which is the MAC address of the target AP and clients MAC address using that we can do deauthentication attack using aireplay-ng And disconnect the client from it’s main AP and as we have spoofed the name we have to wait for the client to connect back to our fake AP and input the credential and as soon he will put the credential we will have that in our radius server logs this attack is also known as Evil Twin.</p>
<br>Now we will mimic our self as a target client and try to connect to our fake AP
<br>![8](https://teckk2.github.io/assets/images/Wifi/26.PNG)
<br>![9](https://teckk2.github.io/assets/images/Wifi/27.PNG)
<br>Now try to crack it with a tool named asleap in which the flag of **[–C]** will represent the Challenge parameter and **[-R]** will represent response and maybe many of you don’t know we used **[–W-]** to get the wordlist from whatever come from pipe, which is rockyou.txt
<br>![10](https://teckk2.github.io/assets/images/Wifi/28.PNG)
<br>And within a sec we can crack the password, but this is a very simple password which is easy to crack, 
Let’s try with some more complex password this time
<br>![11](https://teckk2.github.io/assets/images/Wifi/29.PNG)
<br>![12](https://teckk2.github.io/assets/images/Wifi/30.PNG)
<br>![13](https://teckk2.github.io/assets/images/Wifi/31.PNG)
<br>Within couple of sec it cracked the password, but what if the password is not listed in any wordlist, then we have to create our own rainbow table, with the combination of alphanumeric + special char
<br>![14](https://teckk2.github.io/assets/images/Wifi/32.PNG)
<br>For that we can use this charset.txt to generate the list, we will use crunch to generate our own rainbow table
<br>Take an example the password is = **P@ssword@123** and which is not available in rockyou.txt or in any of the list now we have to create our own list.
<br>![15](https://teckk2.github.io/assets/images/Wifi/33.PNG)
<br>In this way we can try to crack the password, but this process will take a lot of time depending upon your password strengths so you can try this yourself with your custom password. 

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>






